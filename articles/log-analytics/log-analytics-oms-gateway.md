---
title: "aaaConnect computadores tooOMS usando Olá OMS Gateway | Microsoft Docs"
description: "Conecte seus dispositivos gerenciados pelo OMS e computadores monitorados pelo Operations Manager com o serviço OMS Olá OMS Gateway toosend dados toohello quando eles não têm acesso à Internet."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ae9a1623-d2ba-41d3-bd97-36e65d3ca119
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: magoedte
ms.openlocfilehash: 0cfa8f2fb66016e494f22c780e328be472b5fdee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-computers-without-internet-access-toooms-using-hello-oms-gateway"></a>Conectar computadores sem tooOMS de acesso à Internet usando Olá Gateway do OMS

Este documento descreve como o OMS gerenciados e computadores monitorados do System Center Operations Manager podem enviar serviço do OMS toohello dados quando eles não têm acesso à Internet. Olá Gateway do OMS, que é um proxy de encaminhamento de HTTP que dá suporte a HTTP túnel usando o comando de conexão HTTP hello, pode coletar dados e envie-o serviço OMS toohello em seu nome.  

Olá OMS Gateway oferece suporte a:

* Runbook Workers Híbridos da Automação do Azure  
* Computadores Windows com hello Microsoft Monitoring Agent diretamente conectados tooan espaço de trabalho do OMS
* Computadores Linux com hello agente do OMS para Linux conectado diretamente tooan espaço de trabalho do OMS  
* System Center Operations Manager 2012 SP1 com UR7, Operations Manager 2012 R2 com UR3 ou grupo de gerenciamento do Operations Manager 2016 integrado ao OMS.  

Se suas políticas de segurança de TI não permitir que os computadores em sua toohello de tooconnect de rede da Internet, como o ponto de venda (PDV) dispositivos ou servidores que oferecem suporte a serviços de TI, mas você precisa tooconnect toomanage tooOMS-las e monitorá-los, eles podem ser configurados toocommunicate diretamente com a configuração de tooreceive de Gateway de OMS do hello e encaminhar os dados em seu nome.  Se esses computadores são configurados com toodirectly de agente do OMS Olá conecte tooan espaço de trabalho do OMS, todos os computadores em vez disso, se comunicará com hello Gateway do OMS.  gateway Olá transfere dados de saudação agentes tooOMS diretamente, ela não analisa Olá dados em trânsito.

Quando um grupo de gerenciamento do Operations Manager está integrado com o OMS, servidores de gerenciamento de saudação podem ser configurado tooconnect toohello informações de configuração do Gateway do OMS tooreceive e enviar os dados coletados dependendo da solução Olá que você habilitou.  Agentes do Operations Manager enviam alguns dados, como alertas do Operations Manager, avaliação de configuração, o espaço de instância e servidor de gerenciamento de toohello de dados de capacidade. Outros dados de alto volume, como eventos de segurança, desempenho e logs do IIS são enviados diretamente toohello Gateway do OMS.  Se você tiver um ou mais servidores de Gateway do Operations Manager implantados na rede de Perímetro ou outros toomonitor rede isolada sistemas não confiáveis, ele não pode se comunicar com um Gateway do OMS.  Servidores do Operations Manager Gateway podem somente tooa gerenciamento servidor de relatório.  Quando um grupo de gerenciamento do Operations Manager é configurado toocommunicate com hello Gateway do OMS, informações de configuração de proxy de saudação são automaticamente distribuído tooevery computador gerenciado por agente configurado toocollect dados para análise de Log, mesmo se configuração de saudação está vazia.    

tooprovide alta disponibilidade para direto conectado ou grupos de gerenciamento de operações que se comunicam com o OMS por meio do gateway hello, você pode usar tooredirect de balanceamento de carga de rede e distribuir o tráfego de saudação em vários servidores de gateway.  Se um servidor de gateway falhar, o tráfego de saudação é nó disponível tooanother redirecionado.  

É recomendável que você instale o agente do OMS Olá no computador Olá executando Olá OMS Gateway software toomonitor Olá Gateway do OMS e analisar dados de desempenho ou eventos. Além disso, Olá agente ajuda a saudação OMS Gateway identificar pontos de extremidade do serviço Olá precisa toocommunicate com.

Cada agente deve ter o gateway de tooits de conectividade de rede para que os agentes automaticamente podem transferir dados tooand de gateway de saudação. Instalação do gateway Olá em um controlador de domínio não é recomendado.

Olá diagrama a seguir mostra o fluxo de dados de tooOMS agentes direto usando o servidor de gateway hello.  Os agentes devem ter sua correspondência de configuração de proxy Olá mesmo Olá porta OMS Gateway é configurado toocommunicate com tooOMS.  

![diagrama Comunicação do agente direto com o OMS](./media/log-analytics-oms-gateway/oms-omsgateway-agentdirectconnect.png)

Olá diagrama a seguir mostra o fluxo de dados de um tooOMS de grupo de gerenciamento do Operations Manager.   

![Diagrama Comunicação do Operations Manager com o OMS](./media/log-analytics-oms-gateway/oms-omsgateway-opsmgrconnect.png)

## <a name="prerequisites"></a>Pré-requisitos

Ao designar uma saudação do computador toorun Gateway do OMS, este computador deve ter o seguinte hello:

* Windows 10, Windows 8.1, Windows 7
* Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008
* .NET Framework 4.5
* Mínimo de processador de 4 núcleos e 8 GB de memória

### <a name="language-availability"></a>Disponibilidade de idiomas

Olá OMS Gateway está disponível em Olá idiomas a seguir:

- Chinês (Simplificado)
- Chinês (Tradicional)
- Tcheco
- Holandês
- Inglês
- Francês
- Alemão
- Húngaro
- Italiano
- Japonês
- Coreano
- Polonês
- Português (Brasil)
- Português (Portugal)
- Russo
- Espanhol (internacional)

## <a name="download-hello-oms-gateway"></a>Baixar Olá Gateway do OMS

Há três maneiras tooget Olá versão mais recente do arquivo de configuração de Gateway do OMS hello.

1. Download de saudação [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=54443).

2. Baixe no portal do OMS hello.  Depois que você entrar no espaço de trabalho OMS tooyour, navegue muito**configurações** > **fontes conectadas** > **servidores Windows** e clique em **Baixar OMS Gateway**.

3. Download de saudação [portal do Azure](https://portal.azure.com).  Depois de entrar:  

   1. Navegue Olá lista de serviços e, em seguida, selecione **análise de Log**.  
   2. Selecione um espaço de trabalho.
   3. Na folha do espaço de trabalho, em **Geral**, clique em **Início Rápido**.
   4. Em **escolha um espaço de trabalho de toohello de tooconnect de fonte de dados**, clique em **computadores**.
   5. Em Olá **agente direto** folha, clique em **baixar OMS Gateway**.<br><br> ![Baixar Gateway do OMS](./media/log-analytics-oms-gateway/download-gateway.png)


## <a name="install-hello-oms-gateway"></a>Instalar Olá Gateway do OMS

tooinstall um gateway, execute Olá etapas a seguir.  Se você instalou uma versão anterior, anteriormente denominado *encaminhador de análise de Log*, ele será atualizado toothis versão.  

1. Na pasta de destino hello, clique duas vezes em **Gateway.msi OMS**.
2. Em Olá **bem-vindo** , clique em **próximo**.<br><br> ![Assistente de Instalação do Gateway](./media/log-analytics-oms-gateway/gateway-wizard01.png)<br>
3. Em Olá **contrato de licença** página, selecione **aceito os termos de saudação de contrato de licença de saudação** tooagree toohello EULA e, em seguida, clique em **próximo**.
4. Em Olá **endereço de porta e o proxy** página:
   1. Tipo hello TCP porta número toobe usada para o gateway de saudação. A instalação configura uma regra de entrada com esse número de porta no firewall do Windows.  valor padrão de saudação é 8080.
      intervalo válido de saudação do número de porta de saudação é 1 a 65535. Se a entrada de saudação não estiver nesse intervalo, uma mensagem de erro é exibida.
   2. Opcionalmente, se hello, onde é gateway de saudação do servidor instalado necessidades toocommunicate através de um proxy, digite o endereço de proxy Olá onde Olá gateway precisa ser tooconnect. Por exemplo: `http://myorgname.corp.contoso.com:80`.  Se estiver vazio, o gateway Olá tentará tooconnect toohello Internet diretamente.  Se o servidor proxy exigir autenticação, insira um nome de usuário e senha.<br><br> ![Configuração de proxy do Assistente de Gateway](./media/log-analytics-oms-gateway/gateway-wizard02.png)<br>   
   3. Clique em **Avançar**.
5. Se você não tiver o Microsoft Update estiver habilitado, a página do Microsoft Update Olá aparece onde você pode escolher tooenable-lo. Faça uma seleção e clique em **Avançar**. Caso contrário, prossiga toohello próxima etapa.
6. Em Olá **pasta de destino** página, deixe saudação padrão C:\Program Files\OMS Gateway ou tipo hello local da pasta onde você deseja tooinstall gateway e, em seguida, clique em **próximo**.
7. Em Olá **tooinstall pronto** , clique em **instalar**. Controle de conta de usuário podem ser exibidos solicitante tooinstall de permissão. Nesse caso, clique em **Sim**.
8. Depois que Instalação estiver finalizada, clique em **Concluir**. Você pode verificar se o serviço de Olá está em execução, abrindo o snap-in do Services. msc hello e verifique **OMS Gateway** aparece na lista de saudação de serviços e status é **executando**.<br><br> ![Serviços – Gateway do OMS](./media/log-analytics-oms-gateway/gateway-service.png)  

## <a name="configure-network-load-balancing"></a>Configurar o balanceamento de carga de rede
Você pode configurar o gateway de saudação para alta disponibilidade usando o balanceamento de rede (NLB) usando o Microsoft rede NLB Balanceamento de carga () ou balanceadores de carga com base em hardware.  Olá balanceador de carga gerencia o tráfego redirecionando Olá solicitado conexões do hello agentes do OMS ou servidores de gerenciamento do Operations Manager em seus nós. Se um servidor de Gateway falhar, o tráfego Olá obtém nós de tooother redirecionado.

toolearn como toodesign e implantar uma cluster de balanceamento de carga de rede Windows Server 2016, consulte [balanceamento de carga de rede](https://technet.microsoft.com/windows-server-docs/networking/technologies/network-load-balancing).  Olá etapas a seguir descrevem como tooconfigure uma rede do Microsoft cluster balanceamento de carga.  

1.  Faça logon no servidor do Windows hello que seja membro do cluster NLB Olá com uma conta administrativa.  
2.  Abra o Gerenciador de Balanceamento de Carga de Rede no gerenciador de servidores, clique em **Ferramentas**e clique em **Gerenciador de Balanceamento de Carga de Rede**.
3. tooconnect um servidor de Gateway de OMS com hello Microsoft Monitoring Agent instalado, clique no endereço IP do cluster Olá e clique **tooCluster Adicionar Host**.<br><br> ![Gerenciador de balanceamento de carga de Rede – Adicionar Host tooCluster](./media/log-analytics-oms-gateway/nlb02.png)<br>
4. Insira o endereço IP de saudação saudação do servidor de gateway que você deseja tooconnect.<br><br> ![Gerenciador de balanceamento de carga de Rede – Adicionar Host tooCluster: conectar-se](./media/log-analytics-oms-gateway/nlb03.png)

## <a name="configure-oms-agent-and-operations-manager-management-group"></a>Configurar agente do OMS e grupo de gerenciamento do Operations Manager
Olá seção a seguir inclui as etapas sobre como tooconfigure diretamente conectadas Azure Automation Hybrid Runbook Workers, um grupo de gerenciamento do Operations Manager ou agentes do OMS com hello OMS Gateway toocommunicate com o OMS.  

toounderstand requisitos e etapas sobre como tooinstall Olá agente do OMS em computadores com Windows se conectar diretamente a tooOMS, consulte [Windows conectar computadores tooOMS](log-analytics-windows-agents.md) ou para Linux, consulte computadores [conectar computadores Linux tooOMS](log-analytics-linux-agents.md).

### <a name="configuring-hello-oms-agent-and-operations-manager-toouse-hello-oms-gateway-as-a-proxy-server"></a>Configurando o agente do OMS hello e do Operations Manager toouse Olá OMS Gateway como um servidor proxy

### <a name="configure-standalone-oms-agent"></a>Configurar agente do OMS autônomo
Consulte [definir configurações de proxy e firewall com hello Microsoft Monitoring Agent](log-analytics-proxy-firewall.md) para obter informações sobre como configurar um toouse um servidor proxy, que nesse caso é o gateway de saudação do agente.  Se você implantar vários servidores de gateway por trás de um balanceador de carga de rede, configuração de proxy de agente OMS Olá é endereço IP virtual de saudação do hello NLB:<br><br> ![Propriedades do Microsoft Monitoring Agent – Configurações de Proxy](./media/log-analytics-oms-gateway/nlb04.png)

### <a name="configure-operations-manager---all-agents-use-hello-same-proxy-server"></a>Configurar o Operations Manager - todos os agentes usam Olá mesmo servidor proxy
Configurar o servidor de gateway do Operations Manager tooadd hello.  Olá Operations Manager, configuração de proxy é automaticamente aplicado agentes tooall reporting tooOperations Gerenciador, mesmo se a configuração de saudação está vazia.

toouse Olá Gateway toosupport Operations Manager, você deve ter:

* Microsoft Monitoring Agent (agent versão – **8.0.10900.0** e posterior) instalado no servidor de Gateway hello e configurado para espaços de trabalho do OMS Olá com o qual você deseja toocommunicate.
* gateway Olá deve ter conectividade com a Internet ou ser o servidor proxy tooa conectado que faz.

> [!NOTE]
> Se você não especificar um valor para o gateway hello, valores em branco são enviados por push agentes tooall.


1. Console do Operations Manager Olá aberto e, em **Operations Management Suite**, clique em **Conexão** e, em seguida, clique em **configurar servidor Proxy**.<br><br> ![Operations Manager – Configurar o Servidor Proxy](./media/log-analytics-oms-gateway/scom01.png)<br>
2. Selecione **usar uma tooaccess saudação do servidor proxy Operations Management Suite** e, em seguida, digite o endereço IP de saudação do servidor de Gateway do OMS de saudação ou endereço IP virtual da saudação NLB. Certifique-se de que você inicie com hello `http://` prefixo.<br><br> ![Operations Manager – endereço do servidor proxy](./media/log-analytics-oms-gateway/scom02.png)<br>
3. Clique em **Concluir**. O servidor do Operations Manager está conectado tooyour espaço de trabalho do OMS.

### <a name="configure-operations-manager---specific-agents-use-proxy-server"></a>Configurar o Operations Manager - agentes específicos usam servidor proxy
Para ambientes grandes ou complexos, convém apenas específico servidores (ou grupos) toouse Olá servidor de Gateway do OMS.  Para esses servidores, você não pode atualizar Olá agente diretamente como esse valor é substituído pelo valor global de Olá Olá grupo de gerenciamento do Operations Manager.  Em vez disso, você precisa toooverride Olá regra usada toopush esses valores.

> [!NOTE]
> Essa mesma técnica de configuração pode ser usada tooallow uso de saudação de vários servidores de Gateway do OMS em seu ambiente.  Por exemplo, você pode exigir específico toobe de servidores de Gateway do OMS especificado em uma base por região.

1. Console do Operations Manager abertos hello e selecione Olá **criação** espaço de trabalho.  
2. No espaço de trabalho de criação de saudação, selecione **regras** e clique em Olá **escopo** botão na barra de ferramentas do Operations Manager hello. Se esse botão não estiver disponível, verifique toomake se você tem um objeto, não uma pasta, selecionado no painel de monitoramento de saudação. Olá **delimitar objetos do pacote de gerenciamento** caixa de diálogo exibe uma lista de classes comuns de destino, grupos ou objetos.
3. Tipo **serviço de integridade** em Olá **procure** campo e selecione-o na lista de saudação.  Clique em **OK**.  
4. Pesquise a regra de saudação **regra de configuração de Proxy do Advisor** e em ferramentas do console de operações de saudação, clique em **substitui** e aponte muito**substituição Olá Rule\For um objeto específico da classe: integridade Serviço** e selecione um objeto específico da lista de saudação.  Opcionalmente, você pode criar um grupo personalizado que contém o objeto de serviço de integridade de saudação de servidores Olá você deseja tooapply tooand Esta substituição, aplique Olá substituição toothat grupo.
5. Em Olá **substituir propriedades** caixa de diálogo, clique em tooplace marcar Olá **substituir** toohello próxima coluna **WebProxyAddress** parâmetro.  Em Olá **valor de substituição** , digite a URL de Olá Olá OMS Gateway server garante que começam com hello `http://` prefixo.
   >[!NOTE]
   > Regra de saudação tooenable não é necessário pois ele já é gerenciado automaticamente com uma substituição contida no Microsoft System Center Advisor substituição de referência segura da Olá gerenciamento pacote direcionamento Olá grupo de servidor de monitoramento do Microsoft System Center Advisor.
   >
6. Selecione um pacote de gerenciamento de saudação **selecione o pacote de gerenciamento de destino** lista ou crie um novo pacote de gerenciamento sem lacre clicando **novo**.
7. Quando você concluir as alterações, clique em **OK**.

### <a name="configure-for-automation-hybrid-workers"></a>Configurar para hybrid workers de automação
Se você tiver automação Hybrid Runbook Workers em seu ambiente, Olá etapas a seguir fornece soluções alternativas manuais, temporário tooconfigure Olá Gateway toosupport-los.

Olá etapas a seguir, é necessário tooknow Olá região do Azure onde reside a conta de automação de saudação. local da saudação toolocate:

1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. Selecione o serviço de automação do Azure hello.
3. Selecione a conta de automação do Azure apropriada hello.
4. Exiba sua região em **Local**.<br><br> ![Portal do Azure – local da conta de Automação](./media/log-analytics-oms-gateway/location.png)  

Use Olá tabelas tooidentify Olá URL para cada local a seguir:

**URLs de serviço de dados de tempo de execução do trabalho**

| **local** | **URL** |
| --- | --- |
| Centro-Norte dos EUA |ncus-jobruntimedata-prod-su1.azure-automation.net |
| Europa Ocidental |we-jobruntimedata-prod-su1.azure-automation.net |
| Centro-Sul dos Estados Unidos |scus-jobruntimedata-prod-su1.azure-automation.net |
| Leste dos EUA 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| Centro do Canadá |cc-jobruntimedata-prod-su1.azure-automation.net |
| Norte da Europa |ne-jobruntimedata-prod-su1.azure-automation.net |
| Sudeste da Ásia |sea-jobruntimedata-prod-su1.azure-automation.net |
| Índia Central |cid-jobruntimedata-prod-su1.azure-automation.net |
| Japão |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Austrália |ase-jobruntimedata-prod-su1.azure-automation.net |

**URLs de serviço do agente**

| **local** | **URL** |
| --- | --- |
| Centro-Norte dos EUA |ncus-agentservice-prod-1.azure-automation.net |
| Europa Ocidental |we-agentservice-prod-1.azure-automation.net |
| Centro-Sul dos Estados Unidos |scus-agentservice-prod-1.azure-automation.net |
| Leste dos EUA 2 |eus2-agentservice-prod-1.azure-automation.net |
| Centro do Canadá |cc-agentservice-prod-1.azure-automation.net |
| Norte da Europa |ne-agentservice-prod-1.azure-automation.net |
| Sudeste da Ásia |sea-agentservice-prod-1.azure-automation.net |
| Índia Central |cid-agentservice-prod-1.azure-automation.net |
| Japão |jpe-agentservice-prod-1.azure-automation.net |
| Austrália |ase-agentservice-prod-1.azure-automation.net |

Se o computador é registrado como um Hybrid Runbook Worker automaticamente para aplicação de patch usando a solução de gerenciamento de atualizações de saudação, siga estas etapas:

1. Adicione lista de Host permitidos toohello do URLs de serviço de dados de tempo de execução do trabalho Olá em Olá Gateway do OMS. Por exemplo: `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
2. Reinicie o serviço de Gateway do OMS de saudação usando Olá cmdlet do PowerShell a seguir:`Restart-Service OMSGatewayService`

Se o computador estiver tooAzure onboard automação usando o cmdlet de registro de Hybrid Runbook Worker hello, siga estas etapas:

1. Adicione lista de Host permitidos Olá agent service registro URL toohello em Olá Gateway do OMS. Por exemplo: `Add-OMSGatewayAllowedHost ncus-agentservice-prod-1.azure-automation.net`
2. Adicione lista de Host permitidos toohello do URLs de serviço de dados de tempo de execução do trabalho Olá em Olá Gateway do OMS. Por exemplo: `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
3. Reinicie o serviço de Gateway de OMS do hello.
    `Restart-Service OMSGatewayService`

## <a name="useful-powershell-cmdlets"></a>Cmdlets úteis do PowerShell
Cmdlets pode ajudá-lo a concluir tarefas que são definições de configuração do Gateway de OMS Olá tooupdate necessário. Antes de você usá-los, não se esqueça de:

1. Instale Olá OMS Gateway (MSI).
2. Abra uma janela do console do PowerShell.
3. módulo de saudação tooimport, digite o seguinte comando:`Import-Module OMSGateway`
4. Se nenhum erro ocorreu na etapa anterior hello, módulo Olá foi importado com êxito e Olá cmdlets podem ser usados. Digite `Get-Module OMSGateway`
5. Depois de fazer alterações usando os cmdlets de saudação, certifique-se de que você reinicie o serviço de Gateway hello.

Se você receber um erro na etapa 3, o módulo de saudação não foi importado. Erro de saudação pode ocorrer quando o PowerShell é um módulo de saudação toofind não é possível. Você pode ser encontrado no caminho de instalação do Gateway Olá: *C:\Program Files\Microsoft OMS Gateway\PowerShell*.

| **Cmdlet** | **Parâmetros** | **Descrição** | **Exemplo** |
| --- | --- | --- | --- |  
| `Get-OMSGatewayConfig` |Chave |Obtém a configuração do serviço Olá Olá |`Get-OMSGatewayConfig` |  
| `Set-OMSGatewayConfig` |Chave (obrigatória) <br> Valor |Configuração do serviço de saudação de Olá alterações |`Set-OMSGatewayConfig -Name ListenPort -Value 8080` |  
| `Get-OMSGatewayRelayProxy` | |Obtém o endereço de saudação do proxy de retransmissão (upstream) |`Get-OMSGatewayRelayProxy` |  
| `Set-OMSGatewayRelayProxy` |Endereço<br> Nome de Usuário<br> Senha |Define hello endereço (e credenciais) do proxy de retransmissão (upstream) |1. Define um proxy de retransmissão e uma credencial:<br> `Set-OMSGatewayRelayProxy`<br>`-Address http://www.myproxy.com:8080`<br>`-Username user1 -Password 123` <br><br> 2. Define um proxy de resposta que não precise de autenticação: `Set-OMSGatewayRelayProxy`<br> `-Address http://www.myproxy.com:8080` <br><br> 3. Limpar Olá retransmissão configuração do proxy:<br> `Set-OMSGatewayRelayProxy` <br> `-Address ""` |  
| `Get-OMSGatewayAllowedHost` | |Obtém Olá atualmente permitidos host (somente hello host permitidos configurado localmente, não inclui hosts permitidos baixados automaticamente) |`Get-OMSGatewayAllowedHost` |
| `Add-OMSGatewayAllowedHost` |Host (obrigatório) |Adiciona Olá host toohello lista de permitidos |`Add-OMSGatewayAllowedHost -Host www.test.com` |  
| `Remove-OMSGatewayAllowedHost` |Host (obrigatório) |Remove host Olá Olá lista de permitidos |`Remove-OMSGatewayAllowedHost`<br> `-Host www.test.com` |  
| `Add-OMSGatewayAllowedClientCertificate` |Assunto (obrigatório) |Adiciona um certificado de cliente de Olá assunto toohello lista de permitidos |`Add-OMSGatewayAllowed`<br>`ClientCertificate` <br> `-Subject mycert` |  
| `Remove-OMSGatewayAllowedClientCertificate` |Assunto (obrigatório) |Remove a entidade do certificado de cliente de saudação Olá lista de permissões |`Remove-OMSGatewayAllowed` <br> `ClientCertificate` <br> `-Subject mycert` |  
| `Get-OMSGatewayAllowedClientCertificate` | |Obtém Olá atualmente permitidos cliente entidades do certificado (apenas localmente Olá configurada assuntos permitidos, não inclui entidades permitidas baixadas automaticamente) |`Get-`<br>`OMSGatewayAllowed`<br>`ClientCertificate` |  

## <a name="troubleshooting"></a>Solucionar problemas
eventos de toocollect registrados pelo gateway hello, você precisa tooalso têm o agente do OMS Olá instalado.<br><br> ![Visualizador de Eventos – Log do Gateway do OMS](./media/log-analytics-oms-gateway/event-viewer.png)

**IDs e descrições dos eventos de Gateway do OMS**

Olá tabela a seguir mostra Olá IDs de eventos e descrições para eventos de Log de OMS do Gateway.

| **ID** | **Descrição** |
| --- | --- |
| 400 |Qualquer erro de aplicativo que não tenha uma ID específica |
| 401 |Configuração incorreta. Por exemplo: listenPort = "texto" em vez de um número inteiro |
| 402 |Exceção ao analisar mensagens de handshake TLS |
| 403 |Rede de rede. Por exemplo: não é possível conectar o servidor tootarget |
| 100 |Informações gerais |
| 101 |Serviço iniciado |
| 102 |Serviço interrompido |
| 103 |Comando HTTP CONNECT recebido do cliente |
| 104 |Não é um comando HTTP CONNECT |
| 105 |Servidor de destino não está na lista de permitidos ou Olá destino porta não é segura (443) <br> <br> Certifique-se de que Olá MMA o agente no servidor de Gateway e agentes Olá Olá Gateway se comunicando são conectado toohello mesmo espaço de trabalho de análise de Log. |
| 105 |ERRO TcpConnection – Certificado de cliente inválido: CN=Gateway <br><br> Verifique se: <br>    <br> &#149; Você está usando um Gateway com o número de versão 1.0.395.0 ou superior. <br> &#149; Olá MMA agente no servidor de Gateway e agentes Olá Olá Gateway se comunicando são conectado toohello mesmo espaço de trabalho de análise de Log. |
| 106 |Qualquer motivo pelo qual a sessão do TLS Olá é suspeito e rejeitados |
| 107 |sessão do TLS Olá foi verificada |

**Toocollect de contadores de desempenho**

Olá tabela a seguir mostra contadores de desempenho de saudação disponíveis para Olá Gateway do OMS. Você pode adicionar contadores hello usando o Monitor de desempenho.

| **Nome** | **Descrição** |
| --- | --- |
| Gateway do OMS/Conexão de Cliente Ativo |Número de conexões de rede de cliente ativo (TCP) |
| Gateway do OMS/Contagem de Erro |Número de erros |
| Gateway do OMS/Cliente Conectado |Número de clientes conectados |
| Gateway do OMS/Contagem de Rejeição |Número de rejeições devido a erro de validação de TLS tooany |

![Contadores de desempenho do Gateway OMS](./media/log-analytics-oms-gateway/counters.png)

## <a name="get-assistance"></a>Obter assistência
Quando você estiver conectado toohello portal do Azure, você pode criar uma solicitação de assistência com hello OMS Gateway ou qualquer outro serviço do Azure ou recurso de um serviço.
toorequest assistência, clique Olá símbolo de ponto de interrogação no canto superior direito de saudação do portal hello e, em seguida, clique em **nova solicitação de suporte**. Em seguida, conclua o novo formulário de solicitação de suporte hello.

![Nova solicitação de suporte](./media/log-analytics-oms-gateway/support.png)

Você também pode deixar seus comentários sobre o OMS ou análise de Log em Olá [Fórum de comentários do Microsoft Azure](https://feedback.azure.com/forums/267889).

## <a name="next-steps"></a>Próximas etapas
* [Adicionar fontes de dados](log-analytics-data-sources.md) toocollect dados Olá fontes conectadas em seu espaço de trabalho do OMS e armazená-la no repositório do OMS hello.
