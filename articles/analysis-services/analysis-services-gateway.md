---
title: gateway de dados local aaaOn | Microsoft Docs
description: "É necessário se o servidor do Analysis Services no Azure conectar fontes de dados locais tooon um gateway local."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a>Conectando a fontes de dados locais tooon com Gateway de dados local do Azure
gateway de dados local Olá atua como uma ponte, fornecendo uma transferência de dados segura entre fontes de dados locais e os servidores de serviços de análise do Azure na nuvem hello. Adição tooworking com vários servidores de serviços de análise do Azure em hello mesma região, a versão mais recente de saudação do gateway Olá também funciona com os aplicativos lógicos do Azure e Microsoft Flow, aplicativos do Power e Power BI. Você pode associar vários serviços em Olá mesma região com um único gateway. 

 Serviços de análise do Azure exige um recurso de gateway no hello mesma região. Por exemplo, se você tiver servidores do Azure Analysis Services na região do Leste dos EUA 2 Olá, você precisa de um recurso de gateway na região Leste dos EUA 2 de saudação. Vários servidores no Leste dos EUA 2 podem usar Olá mesmo gateway.

Obtendo a instalação com Olá Olá de gateway primeira vez que é um processo de quatro partes:

- **Baixar e executar a instalação** – esta etapa instala um serviço de gateway em um computador em sua organização.

- **Registre seu gateway** - nesta etapa, você especificar um nome e recuperação de chave para o gateway e selecione uma região, Registrando seu gateway Olá serviço de nuvem do Gateway.

- **Criar um recurso de gateway no Azure** – nesta etapa, você cria um recurso de gateway em sua assinatura do Azure.

- **Conectar seus recursos de servidores de gateway tooyour** -uma vez que um recurso de gateway na sua assinatura, você pode começar a se conectar a servidores tooit.

Uma vez que um recurso de gateway configurado para a sua assinatura, você pode conectar vários servidores e outros serviços tooit. Você só precisa tooinstall um gateway diferente e cria recursos adicionais do gateway se você tiver servidores ou outros serviços em uma região diferente.

tooget iniciado imediatamente, consulte [instalar e configurar o gateway de dados no local](analysis-services-gateway-install.md).

## <a name="how-it-works"> </a>Como funciona
gateway de saudação instalar em um computador em sua organização é executado como um serviço do Windows, **gateway de dados no local**. Esse serviço local está registrado com hello serviço de nuvem do Gateway por meio do barramento de serviço do Azure. Em seguida, você cria um Serviço de Nuvem do Gateway do recurso de gateway para sua assinatura do Azure. Os serviços de análise do Azure são servidores conectados tooyour recursos de gateway. Quando modelos em seu tooyour do servidor necessidade tooconnect fontes de dados para processamento de consultas ou no local, uma consulta e dados fluxo percorrerá Olá recurso de gateway, barramento de serviço do Azure, Olá o serviço de gateway de dados local no local e suas fontes de dados. 

![Como funciona](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

Fluxo de dados e consultas:

1. Uma consulta é criada pelo serviço de nuvem Olá com credenciais Olá criptografado para fonte de dados do local de saudação. Em seguida, esta foi enviada fila tooa Olá gateway tooprocess.
2. serviço de nuvem do gateway Olá analisa consulta hello e envia Olá solicitação toohello [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).
3. gateway de dados local Olá sonda hello Azure Service Bus para solicitações pendentes.
4. Olá gateway obtém Olá consulta, descriptografa Olá credenciais e conecta-se a fontes de dados toohello com essas credenciais.
5. gateway Olá envia a fonte de dados de toohello Olá consulta para execução.
6. resultados de saudação são enviados da fonte de dados hello, gateway toohello voltar e, em seguida, no serviço de nuvem hello e o servidor.

## <a name="windows-service-account"> </a>Conta de Serviço Windows
Olá, gateway de dados local é configurado toouse *NT SERVICE\PBIEgwService* para credenciais de logon do serviço de Windows hello. Por padrão, ele tem Olá direito de Logon como um serviço; no contexto de saudação da máquina de saudação que você está instalando gateway hello. Essa credencial não é Olá conta usada mesmo local tooon tooconnect fontes de dados ou sua conta do Azure.  

Se você tiver problemas com o servidor proxy devido tooauthentication, talvez você queira toochange Windows hello usuário de domínio de tooa de conta de serviço ou gerenciados conta de serviço.

## <a name="ports"> </a>Portas
gateway Olá cria uma conexão de saída de tooAzure barramento de serviço. Ele se comunica nas portas de saída: TCP 443 (padrão), 5671, 5672, 9350 a 9354.  Olá gateway não requer portas de entrada.

Recomendamos que você os endereços IP de Olá lista branca para sua região de dados em seu firewall. Você pode baixar Olá [lista de IP de Datacenter do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653). A lista é atualizada semanalmente.

> [!NOTE]
> Endereços de IP de saudação listadas na lista de IP de Datacenter do Azure Olá estão na notação CIDR. Por exemplo, 10.0.0.0/24 significa 10.0.0.0 a 10.0.0.24. Saiba mais sobre Olá [notação CIDR](http://whatismyipaddress.com/cidr).
>
>

Olá seguem usados pelo gateway de saudação de nomes de domínio Olá totalmente qualificado.

| Nomes de domínio | Portas de saída | Descrição |
| --- | --- | --- |
| *.powerbi.com |80 |Instalador do hello toodownload HTTP usado. |
| *.powerbi.com |443 |HTTPS |
| *.analysis.windows.net |443 |HTTPS |
| *.login.windows.net |443 |HTTPS |
| *.servicebus.windows.net |5671-5672 |Advanced Message Queuing Protocol (AMQP) |
| *.servicebus.windows.net |443, 9350-9354 |Ouvintes de Retransmissão do Barramento de Serviço por meio de TCP (requer 443 para aquisição de token de Controle de Acesso) |
| *.frontend.clouddatahub.net |443 |HTTPS |
| *.core.windows.net |443 |HTTPS |
| login.microsoftonline.com |443 |HTTPS |
| *.msftncsi.com |443 |Usado tootest conectividade com a internet se gateway hello está inacessível por Olá serviço do Power BI. |
| *.microsoftonline p.com |443 |Usado para autenticação, dependendo da configuração. |

### <a name="force-https"></a>Forçar comunicação HTTPS com o Barramento de Serviço do Azure
Você pode forçar Olá toocommunicate de gateway com o barramento de serviço do Azure usando HTTPS em vez de direta TCP; No entanto, fazer assim pode reduzir bastante desempenho. Você pode modificar Olá *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* arquivo alterando o valor de saudação do `AutoDetect` muito`Https`. Normalmente, esse arquivo fica localizado em *C:\Arquivos de Programas\Gateway de dados local*.

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <a name="faq"></a>Perguntas frequentes

### <a name="general"></a>Geral

**P**: É necessário um gateway para fontes de dados na nuvem hello, como o banco de dados do SQL Azure? <br/>
**R:** Não. Um gateway se conecta a fontes de dados de locais tooon somente.

**P**: gateway de saudação tem toobe instalado Olá mesmo computador como fonte de dados Olá? <br/>
**R:** Não. gateway de saudação conecta toohello fonte de dados usando as informações de conexão de saudação que foi fornecidas. Considere o gateway hello como um aplicativo cliente nesse sentido. Olá gateway só precisa Olá recurso tooconnect toohello nome do servidor que foi fornecido, normalmente de saudação mesmo rede.

<a name="why-azure-work-school-account"></a>

**P**: por que preciso toouse um trabalho ou escolar toosign de conta no? <br/>
**Um**: somente, você pode usar um trabalho do Azure ou conta escolar quando você instalar o gateway de dados local hello. Sua conta de entrada é armazenada em um locatário gerenciado pelo Azure AD (Azure Active Directory). Geralmente, o nome principal de usuário do sua conta AD do Azure (UPN) corresponde endereço de email de saudação.

**P**: Em que local minhas credenciais são armazenadas? <br/>
**Um**: credenciais de saudação que você inserir para uma fonte de dados são criptografadas e armazenadas em Olá serviço de nuvem do Gateway. as credenciais de saudação são descriptografadas no gateway de dados local hello.

**P**: Há algum requisito de largura de banda de rede? <br/>
**R**: Recomendamos que sua conexão de rede tenha uma boa taxa de transferência. Cada ambiente é diferente e quantidade de saudação do envio de dados afeta os resultados de saudação. Uso da rota expressa pode ajudar a tooguarantee um nível de taxa de transferência entre locais e hello datacenters do Azure.
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
**Um**: em serviços, o gateway de saudação é chamado serviço de gateway de dados local.

**P**: pode Olá serviço Windows do gateway execute com uma conta do Active Directory do Azure? <br/>
**R:** Não. saudação de serviço do Windows deve ter uma conta válida do Windows. Por padrão, o serviço de saudação é executado com hello SID de serviço NT SERVICE\PBIEgwService.

### <a name="high-availability"></a>Alta disponibilidade e recuperação de desastres

**P**: Quais opções estão disponíveis para recuperação de desastre? <br/>
**Um**: você pode usar toorestore de chave de recuperação de saudação ou mover um gateway. Ao instalar o gateway Olá, especifique a chave de recuperação de Olá.

**P**: qual é o benefício de saudação da chave de recuperação Olá? <br/>
**Um**: chave de recuperação Olá fornece uma maneira toomigrate ou recuperar suas configurações de gateway após um desastre.

## <a name="troubleshooting"> </a>Solução de problemas

**P**: como ver quais consultas estão sendo enviadas a fonte de dados local toohello? <br/>
**Um**: você pode habilitar o rastreamento de consulta, que inclui as consultas de saudação que são enviadas. Lembre-se de consulta toochange toohello valor original quando terminado de solução de problemas de rastreamento novamente. Deixar o acompanhamento de consulta ativado cria logs maiores.

Você também pode examinar ferramentas de rastreamento de consultas disponibilizadas por sua fonte de dados. Por exemplo, você pode usar o Extended Events ou o SQL Profiler para SQL Server e Analysis Services.

**P**: onde estão os logs do gateway Olá? <br/>
**R**: Veja Logs, mais adiante neste tópico.

### <a name="update"></a>Atualizar a versão mais recente do toohello

Muitos problemas podem surgir quando a versão do gateway Olá ficará desatualizado. Como boa prática geral, certifique-se de que você use a versão mais recente do hello. Se você não tiver atualizado o gateway Olá por um mês ou mais, talvez considere instalar a versão mais recente saudação do gateway de saudação e ver se você pode reproduzir o problema de saudação.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>Erro: Falha tooadd toogroup de usuário. (-2147463168 PBIEgwService Performance Log Users)

Você pode obter esse erro se você tentar tooinstall gateway de saudação em um controlador de domínio, que não tem suporte. Certifique-se de que você implanta o gateway de saudação em um computador que não seja um controlador de domínio.

## <a name="logs"></a>Logs

Arquivos de log são um recurso importante ao solucionar problemas.

#### <a name="enterprise-gateway-service-logs"></a>Logs de serviço do gateway corporativo

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a>Logs de configuração

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a>Logs de eventos

Você pode encontrar hello logs do Gateway de gerenciamento de dados e PowerBIGateway em **Logs de aplicativos e serviços**.


## <a name="telemetry"></a>Telemetria
Telemetria pode ser usada para monitorar e solucionar problemas. Por padrão

**tooturn na Telemetria**

1.  Verifique o diretório de cliente do gateway do hello local dados no computador de saudação. Normalmente, é **%systemdrive%\Program Files\On-premises data gateway**. Ou, você pode abrir um console de serviços e verifique Olá caminho tooexecutable: uma propriedade de serviço de gateway de dados local hello.
2.  No arquivo de Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config de saudação do diretório do cliente. Altere Olá SendTelemetry configuração tootrue.
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  Salve suas alterações e reiniciar o serviço do Windows hello: serviço de gateway de dados local.




## <a name="next-steps"></a>Próximas etapas
* [Gerenciar o Analysis Services](analysis-services-manage.md)
* [Obter dados do Azure Analysis Services](analysis-services-connect.md)
