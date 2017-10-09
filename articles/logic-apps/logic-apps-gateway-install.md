---
title: "gateway de dados local aaaInstall - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Antes de acessar fontes de dados no local, instalar o gateway de dados de local de saudação para transferência de dados rápida e criptografia entre fontes de dados no local e os aplicativos lógicos"
keywords: "acessar dados, local, transferência de dados, criptografia, fontes de dados"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a>Instalar o gateway de dados do local de saudação para os aplicativos lógicos do Azure

Para que seus aplicativos lógicos podem acessar fontes de dados no local, você deve instalar e configurar o gateway de dados local hello. gateway de saudação atua como uma ponte que fornece transferência de dados rápida e criptografia entre sistemas locais e seus aplicativos lógicos. gateway Olá transmite dados de fontes locais em canais criptografados por meio de saudação do Azure Service Bus. Todo o tráfego originado como proteger o tráfego de saída do agente de gateway de saudação. Saiba mais sobre [como funciona o gateway de dados Olá](#gateway-cloud-service).

gateway Olá dá suporte a fontes de dados de toothese de conexões no local:

*   BizTalk Server 2016
*   DB2  
*   Sistema de Arquivos
*   Informix
*   MQ
*   MySQL
*   Banco de dados Oracle
*   PostgreSQL
*   Servidor de aplicativos SAP 
*   Servidor de mensagens SAP
*   SharePoint
*   SQL Server
*   Teradata

Essas etapas mostram como toofirst instalação Olá no gateway de dados local antes de você [configurar uma conexão entre o gateway hello e seus aplicativos lógicos](./logic-apps-gateway-connection.md). Para obter mais informações sobre os conectores com suporte, consulte [Conectores para Aplicativo Lógico do Azure](https://docs.microsoft.com/azure/connectors/apis-list). 

Para obter informações sobre como toouse Olá gateway com outros serviços, consulte estes artigos:

*   [Gateway de dados local do Microsoft Power BI](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Gateway de dados local do Azure Analysis Services](../analysis-services/analysis-services-gateway.md)
*   [Gateway de dados local do Microsoft Flow](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Gateway de dados local do Microsoft PowerApps](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a>Requisitos

**Mínimos**:

* .NET 4.5 Framework
* Versão de 64 bits do Windows 7 ou Windows Server 2008 R2 (ou posterior)

**Recomendados**:

* CPU de 8 núcleos
* Memória de 8 GB
* Versão de 64 bits do Windows 2012 R2 (ou posterior)

**Considerações importantes**:

* Instale o gateway de dados local Olá somente em um computador local.
Você não pode instalar o gateway de saudação em um controlador de domínio.

   > [!TIP]
   > Você não tem tooinstall gateway de Olá Olá mesmo computador como sua fonte de dados. toominimize latência, você pode instalar o gateway hello mais próximo que tooyour possível fonte de dados ou em Olá mesmo computador, supondo que você tenha permissões.

* Não instale o gateway Olá em um computador que desativa, vai toosleep ou não conecta toohello Internet porque o gateway de saudação não pode ser executado sob essas circunstâncias. Além disso, o desempenho do gateway pode ser reduzido em uma rede sem fio.

* Durante a instalação, você deve entrar com uma [conta corporativa ou de estudante](https://docs.microsoft.com/azure/active-directory/sign-up-organization) gerenciada pelo Azure AD (Azure Active Directory), não uma conta da Microsoft. 

  Você tem toouse Olá mesmo trabalho ou escola saudação do conta posteriormente no Azure portal quando você cria e associar um recurso de gateway a sua instalação do gateway. Você selecionar esse recurso de gateway ao criar conexão Olá entre sua lógica aplicativo e hello local fonte de dados. [Por que eu devo usar uma conta corporativa ou de estudante do Azure AD?](#why-azure-work-school-account)

  > [!TIP]
  > Se você se inscreveu para uma oferta do Office 365 e não forneceu seu email de trabalho real, o endereço de entrada pode ser semelhante a jeff@contoso.onmicrosoft.com. 

* Se você tiver um gateway existente que você deseja configurar com um instalador que é anterior à versão 14.16.6317.4, é possível alterar o local do gateway pelo instalador mais recente de saudação em execução. No entanto, você pode usar o hello mais recente instalador tooset a um novo gateway com local Olá desejado em vez disso.
  
  Se você tiver um instalador do gateway que é anterior à versão 14.16.6317.4, mas você ainda não instalou o gateway ainda, você pode baixar e usar installer mais recente hello.

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a>Instalar o gateway de dados Olá

1.  [Baixe e execute o instalador do gateway Olá em um computador local](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).

2. Leia e aceite os termos de saudação da declaração de privacidade e de uso.

3. Especifique o caminho de saudação no computador local onde você deseja que o gateway de saudação tooinstall.

4. Quando solicitado, entre com sua conta corporativa ou de estudante do Azure, e não com uma conta da Microsoft.

   ![Entrar com a conta corporativa ou de estudante do Azure](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. Agora, registrar o gateway instalado com hello [serviço de nuvem do gateway](#gateway-cloud-service). Escolha **Registrar um novo gateway neste computador**.

   serviço de nuvem do gateway Olá criptografa e armazena suas credenciais da fonte de dados e os detalhes do gateway. 
   o serviço de saudação também encaminha consultas e seus resultados entre seu aplicativo lógico, o gateway de dados local hello e sua fonte de dados no local.

6. Forneça um nome para sua instalação do gateway. Crie uma chave de recuperação, em seguida, confirme sua chave de recuperação. 

   > [!IMPORTANT] 
   > Sua chave de recuperação deve conter pelo menos oito caracteres. Certifique-se de que você salve e manter a chave de saudação em um local seguro. Você também precisa essa chave quando você quiser toomigrate, restaurar ou assumir um gateway existente.

   1. região do toochange saudação padrão para o serviço de nuvem do gateway hello e barramento de serviço do Azure usado pela instalação do gateway, escolha **alteração região**.

      ![Alterar região](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      saudação padrão Olá a região é associado a seu locatário do AD do Azure.

   2. No painel da próxima Olá, abra Olá **selecionar região** muito, escolha uma região diferente.

      ![Selecionar outra região](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      Por exemplo, você pode selecionar Olá mesma região que seu aplicativo lógico, ou para reduzir a latência da fonte de dados de local de tooyour mais próximos do hello selecione região. Seu aplicativo lógico e recurso de gateway podem ter locais diferentes.

      > [!IMPORTANT]
      > Você não pode alterar essa região após a instalação. Esta região também determina e restringe local Olá onde você pode criar hello recursos do Azure para o gateway. Então quando você cria o recurso de gateway no Azure, verifique se local do recurso Olá corresponde região Olá selecionado durante a instalação do gateway.
      > 
      > Se você quiser toouse uma região diferente para o gateway mais tarde, você deve configurar um novo gateway.

   3. Quando estiver pronto, escolha **Concluído**.

7. Agora, siga estas etapas no hello portal do Azure para que você possa [criar um recurso do Azure para seu gateway](../logic-apps/logic-apps-gateway-connection.md). 

Saiba mais sobre [como funciona o gateway de dados Olá](#gateway-cloud-service).

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a>Migrar, restaurar ou assumir um gateway existente

tooperform essas tarefas, você deve ter a chave de recuperação de saudação que foi especificado quando Olá gateway foi instalado.

1. No menu Iniciar do computador, escolha **Gateway de dados local**.

2. Depois de hello instalador abre, entrar com hello mesmo Azure trabalhar ou conta de escola que foi anteriormente usado tooinstall gateway de saudação.

3. Escolha **Migrar, restaurar ou assumir um gateway existente**.

4. Forneça a chave de nome e a recuperação de saudação para gateway Olá que você deseja toomigrate, restauração ou realizar failover.

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a>Reinicie o gateway de saudação

gateway de saudação é executado como um serviço do Windows. Como qualquer outro serviço do Windows, você pode iniciar e parar o serviço de saudação de várias maneiras. Por exemplo, você pode abrir um prompt de comando com permissões elevadas no computador Olá onde o gateway hello está sendo executado e executar esses comandos ou:

* serviço de saudação toostop, execute este comando:
  
    `net stop PBIEgwService`

* serviço de saudação toostart, execute este comando:
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a>Conta de serviço do Windows

gateway de dados local Olá é configurar toouse `NT SERVICE\PBIEgwService` credenciais de logon de serviço para o Windows hello. Por padrão, o gateway Olá tem direito de "Logon como um serviço" hello máquina Olá onde você instala o gateway de saudação.

> [!NOTE]
> Olá conta de serviço do Windows é diferente de saudação conta usada para se conectar a fontes de dados locais tooon e de saudação do Azure ou conta de escola usado toosign nos serviços de toocloud.

## <a name="configure-a-firewall-or-proxy"></a>Configure um firewall ou proxy

gateway Olá cria uma conexão de saída muito [Azure Service Bus](https://azure.microsoft.com/services/service-bus/). tooprovide informações de proxy para o gateway, consulte [definir configurações de proxy](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).

toocheck se seu firewall ou proxy, pode bloquear conexões, confirme se a sua máquina, na verdade, pode se conectar toohello internet e hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/). Em um prompt do PowerShell, execute este comando:

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> Esse comando apenas testa a conectividade de rede e conectividade toohello barramento de serviço do Azure. Para o comando Olá não tem nenhuma toodo com gateway hello ou serviço de nuvem do gateway de saudação que criptografa e armazena suas credenciais e detalhes do gateway. 
>
> Além disso, esse comando só está disponível no Windows Server 2012 R2 ou posterior e no Windows 8.1 ou posterior. Em versões anteriores do sistema operacional, você pode usar o Telnet muito testar a conectividade. Saiba mais sobre [Soluções híbridas e de Barramento de Serviço do Azure](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).

Seus resultados deverão ser exemplo toothis semelhante:

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

Se **TcpTestSucceeded** não está definido muito**True**, você poderá estar bloqueada por um firewall. Se você quiser toobe abrangente, substitua Olá **ComputerName** e **porta** valores com hello listado em [configurar portas](#configure-ports) neste tópico.

firewall de saudação também pode bloquear conexões que hello que Azure Service Bus torna toohello datacenters do Azure. Se essa situação ocorrer, aprovar (desbloquear) todos Olá endereços IP para os data centers em sua região. Para esses endereços IP, [a lista de endereços de IP do Azure de saudação de get aqui](https://www.microsoft.com/download/details.aspx?id=41653).

## <a name="configure-ports"></a>Configure portas

gateway Olá cria uma conexão de saída muito[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) e se comunica nas portas de saída: TCP 443 (padrão), 5671, 5672, 9350 a 9354. gateway de saudação não requer portas de entrada. Saiba mais sobre [Soluções híbridas e de Barramento de Serviço do Azure](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).

| NOMES DE DOMÍNIO | PORTAS DE SAÍDA | DESCRIÇÃO |
| --- | --- | --- |
| *.analysis.windows.net | 443 | HTTPS | 
| *.login.windows.net | 443 | HTTPS | 
| *.servicebus.windows.net | 5671-5672 | Advanced Message Queuing Protocol (AMQP) | 
| *.servicebus.windows.net | 443, 9350-9354 | Ouvintes de Retransmissão do Barramento de Serviço por meio de TCP (requer 443 para aquisição de token de Controle de Acesso) | 
| *.frontend.clouddatahub.net | 443 | HTTPS | 
| *.core.windows.net | 443 | HTTPS | 
| login.microsoftonline.com | 443 | HTTPS | 
| *.msftncsi.com | 443 | Usado tootest conectividade com a internet quando o gateway hello está inacessível por Olá serviço do Power BI. | 

Se você tiver tooapprove endereços IP em vez de domínios hello, você pode baixar e usar o hello [lista de intervalos de IP de Datacenter do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653). Em alguns casos, são feitas conexões do barramento de serviço do Azure Olá com endereço IP em vez de nomes de domínio totalmente qualificado.

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a>Como funciona o gateway de dados Olá?

gateway de dados Olá facilita a comunicação rápida e segura entre sua lógica de aplicativo, serviço de nuvem do gateway hello e sua fonte de dados local. 

![diagram-for-on-premises-data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

Portanto quando o usuário Olá na nuvem Olá interage com um elemento que tenha se conectado tooyour local fonte de dados:

1. serviço de nuvem do gateway Olá cria uma consulta, juntamente com hello criptografado credenciais Olá fonte de dados e envia toohello fila consulta Olá Olá gateway tooprocess.

2. serviço de nuvem do gateway Olá analisa a consulta hello e envia Olá solicitação toohello barramento de serviço do Azure.

3. gateway de dados local Olá sonda hello Azure Service Bus para solicitações pendentes.

4. Olá gateway obtém Olá consulta, descriptografa Olá credenciais e conecta-se a fonte de dados toohello com essas credenciais.

5. gateway Olá envia a fonte de dados de toohello Olá consulta para execução.

6. Olá resultados são enviados da fonte de dados de saudação, gateway toohello back e toohello serviço de nuvem do gateway. Olá serviço de nuvem do gateway, em seguida, usa Olá resultados.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Perguntas frequentes

### <a name="general"></a>Geral

**P**: É necessário um gateway para fontes de dados na nuvem hello, como SQL Azure? <br/>
**R:** Não. Um gateway se conecta a fontes de dados de locais tooon somente.

**P**: gateway de saudação tem toobe instalado Olá mesmo computador como fonte de dados Olá? <br/>
**R:** Não. gateway de saudação conecta toohello fonte de dados usando as informações de conexão de saudação que foi fornecidas. Considere o gateway hello como um aplicativo cliente nesse sentido. gateway Olá precisa apenas Olá recurso tooconnect toohello nome do servidor que foi fornecido.

<a name="why-azure-work-school-account"></a>

**P**: por que deve, use um trabalho do Azure ou de estudante conta toosign em? <br/>
**Um**: somente, você pode usar um trabalho do Azure ou conta escolar quando você instalar o gateway de dados local hello. Sua conta de entrada é armazenada em um locatário gerenciado pelo Azure AD (Azure Active Directory). Geralmente, o nome principal de usuário do sua conta AD do Azure (UPN) corresponde endereço de email de saudação.

**P**: Em que local minhas credenciais são armazenadas? <br/>
**Um**: credenciais de saudação que você inserir para uma fonte de dados são criptografadas e armazenadas no serviço de nuvem do gateway de saudação. as credenciais de saudação são descriptografadas no gateway de dados local hello.

**P**: Há algum requisito de largura de banda de rede? <br/>
**R**: recomendamos que sua conexão de rede tenha uma boa taxa de transferência. Cada ambiente é diferente e quantidade de saudação do envio de dados afeta os resultados de saudação. Uso da rota expressa pode ajudar a tooguarantee um nível de taxa de transferência entre locais e hello datacenters do Azure.
Você pode usar o hello ferramenta de terceiros Azure Speed Test aplicativo toohelp medidor a taxa de transferência.

**P**: o que é a latência de saudação executando consultas tooa fonte de dados do gateway Olá? O que é a arquitetura recomendada Olá? <br/>
**Um**: tooreduce latência de rede, instalar Olá gateway como fonte de dados toohello fechar possível. Se você pode instalar o gateway de saudação na fonte de dados reais hello, essa proximidade minimiza a latência de saudação introduzida. Considere a possibilidade de datacenters Olá muito. Por exemplo, se o serviço usa o datacenter do Oeste dos EUA hello e você tiver o SQL Server hospedado em uma VM do Azure, sua VM do Azure deve estar no hello Oeste dos EUA muito. Essa proximidade minimiza a latência e evita cobranças de egresso em Olá VM do Azure.

**P**: são como os resultados enviados toohello back nuvem? <br/>
**Um**: os resultados são enviados por meio de saudação do Azure Service Bus.

**P**: há qualquer gateway toohello de conexões de entrada da nuvem Olá? <br/>
**R:** Não. gateway de saudação usa conexões de saída tooAzure barramento de serviço.

**P**: O que acontecerá se eu bloquear conexões de saída? O que eu preciso tooopen? <br/>
**Um**: Consulte portas hello e hosts que Olá gateway usa.

**P**: O serviço Windows real de saudação chamado?<br/>
**Um**: em serviços, o gateway de saudação é chamado serviço do Power BI Enterprise Gateway.

**P**: pode Olá serviço Windows do gateway execute com uma conta do Active Directory do Azure? <br/>
**R:** Não. saudação de serviço do Windows deve ter uma conta válida do Windows. Por padrão, o serviço de saudação é executado com hello SID de serviço NT SERVICE\PBIEgwService.

### <a name="high-availability-and-disaster-recovery"></a>Alta disponibilidade e recuperação de desastres

**P**: Quais opções estão disponíveis para recuperação de desastre? <br/>
**Um**: você pode usar toorestore de chave de recuperação de saudação ou mover um gateway. Ao instalar o gateway Olá, especifique a chave de recuperação de Olá.

**P**: qual é o benefício de saudação da chave de recuperação Olá? <br/>
**Um**: chave de recuperação Olá fornece uma maneira toomigrate ou recuperar suas configurações de gateway após um desastre.

**P**: há planos para habilitar cenários de alta disponibilidade com o gateway Olá? <br/>
**Um**: esses cenários são roteiro hello, mas ainda não tem uma linha do tempo.

## <a name="troubleshooting"></a>Solucionar problemas

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

**P**: como ver quais consultas estão sendo enviadas a fonte de dados local toohello? <br/>
**Um**: você pode habilitar o rastreamento de consulta, que inclui as consultas de saudação que são enviadas. Lembre-se de consulta toochange toohello valor original quando terminado de solução de problemas de rastreamento novamente. Deixar o acompanhamento de consulta ativado cria logs maiores.

Você também pode examinar ferramentas de rastreamento de consultas disponibilizadas por sua fonte de dados. Por exemplo, você pode usar o Extended Events ou o SQL Profiler para SQL Server e Analysis Services.

**P**: onde estão os logs do gateway Olá? <br/>
**R**: Consulte Ferramentas mais adiante neste tópico.

### <a name="update-toohello-latest-version"></a>Atualizar a versão mais recente do toohello

Muitos problemas podem surgir quando a versão do gateway Olá ficará desatualizado. Como boa prática geral, certifique-se de que você use a versão mais recente do hello. Se você não tiver atualizado o gateway Olá por um mês ou mais, talvez considere instalar a versão mais recente saudação do gateway de saudação e ver se você pode reproduzir o problema de saudação.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>Erro: Falha tooadd toogroup de usuário. (-2147463168 PBIEgwService Performance Log Users)

Você pode obter esse erro se você tentar tooinstall gateway de saudação em um controlador de domínio, que não tem suporte. Certifique-se de que você implanta o gateway de saudação em um computador que não seja um controlador de domínio.

## <a name="tools"></a>Ferramentas

### <a name="collect-logs-from-hello-gateway-configurer"></a>Coletar logs do configurer de gateway Olá

Você pode coletar vários logs para o gateway de saudação. Inicie sempre com logs Olá!

#### <a name="installer-logs"></a>Logs do instalador

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a>Logs de configuração

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a>Logs de serviço do gateway corporativo

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a>Logs de eventos

Você pode encontrar hello logs do Gateway de gerenciamento de dados e PowerBIGateway em **Logs de aplicativos e serviços**.

### <a name="fiddler-trace"></a>Rastreamento do Fiddler

[Fiddler](http://www.telerik.com/fiddler) é uma ferramenta gratuita da Telerik que monitora o tráfego HTTP. Você pode ver esse tráfego com hello serviço do Power BI de máquina do cliente hello. Esse serviço pode mostrar erros e outras informações relacionadas.

## <a name="next-steps"></a>Próximas etapas
    
* [Conecte-se a dados locais tooon de aplicativos lógicos](../logic-apps/logic-apps-gateway-connection.md)
* [Recursos de integração corporativa](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [Conectores de Aplicativos Lógicos do Azure](../connectors/apis-list.md)
