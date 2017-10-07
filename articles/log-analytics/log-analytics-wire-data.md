---
title: "aaaWire solução de dados na análise de Log | Microsoft Docs"
description: "Dados de transmissão são dados consolidados de rede e de desempenho recebidos de computadores com agentes do OMS, incluindo agentes do Operations Manager e agentes conectados com o Windows. Dados de rede são combinados com sua toohelp de dados de log correlacionar dados."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: adafdf98dfbda9d87759643a1a606a84eafd1348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a>Solução Wire Data 2.0 (Versão Prévia) no Log Analytics

![Símbolo do Wire Data](./media/log-analytics-wire-data/wire-data2-symbol.png)

O Wire Data consiste em dados de desempenho e rede consolidados de computadores com agentes do OMS, incluindo agentes Operations Manager, conectados ao Windows e aos agentes do Linux. Dados de rede são combinados com seu outros toohelp de dados de log correlacionar dados.

Além disso tooOMS agentes, Olá solução durante a transmissão de dados usa agentes Dependency Microsoft que você instala em computadores na sua infraestrutura de TI. Olá em 2 a 3 níveis de dependência agentes monitor rede dados enviados tooand em seus computadores para a rede [modelo OSI](https://en.wikipedia.org/wiki/OSI_model), incluindo Olá diversos protocolos e portas usados. Em seguida, os dados são enviados tooLog análise usando agentes.

> [!NOTE]
> Você não pode adicionar a versão anterior de saudação de espaços de trabalho da toonew solução Olá dados de transmissão. Se você tiver a solução de dados de transmissão original Olá habilitada, você pode continuar toouse-lo. No entanto, toouse 2.0 de dados durante a transmissão, você deve primeiro remover versão original do hello.

Por padrão, o Log Analytics coleta dados registrados para dados de CPU, memória, disco e desempenho de rede dos contadores internos do Windows. Rede e outro conjunto de dados é feita em tempo real para cada agente, incluindo sub-redes e protocolos de nível de aplicativo que está sendo usados pelo computador de saudação. Você pode adicionar outros contadores de desempenho na página de configurações de saudação na guia de Logs de saudação.

Se você usou [sFlow](http://www.sflow.org/) ou outro software com [protocolo NetFlow da Cisco](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), Olá, em seguida, estatísticas e consulte de dados de transmissão de dados será tooyou familiar.

Alguns dos tipos de saudação de consultas de pesquisa de Log internas incluem:

- Agentes que fornecem dados de transmissão
- Endereço IP de agentes que fornecem dados de transmissão
- Comunicações de saída por endereços IP
- Número de bytes enviados por protocolos de aplicativo
- Número de bytes enviados por um serviço de aplicativo
- Bytes recebidos por diferentes protocolos
- Total de bytes enviados e recebidos por versão de IP
- Latência média de conexões que foram medidas de forma confiável
- Processos de computador que iniciaram ou receberam tráfego de rede
- Quantidade de tráfego de rede de um processo

Quando você pesquisa usando dados de transmissão, você pode filtrar e grupo dados tooview informações sobre Olá principais agentes e protocolos. Ou você pode exibir quando determinados computadores (endereços IP/MAC) comunicaram-se entre si, a duração dessa comunicação e a quantidade de dados enviados – basicamente, são exibidos metadados sobre o tráfego de rede, que são baseados em pesquisa.

No entanto, já que você está exibindo metadados, eles não são necessariamente úteis para solução de problemas detalhada. Wire Data no Log Analytics não é uma captura completa dos dados da rede. Portanto, não se destina a uma solução de problemas em profundidade no nível de pacote. Olá vantagem de usar o agente hello, em comparação com os métodos de coleta tooother, é que você não tem tooinstall dispositivos, reconfigurar comutadores de rede nem realizar configurações complicadas. Dados de transmissão são simplesmente baseados em agente – instalar o agente de saudação em um computador e ele vai monitorar seu próprio tráfego de rede. Outra vantagem é que quando você quiser toomonitor cargas de trabalho em execução em provedores de nuvem, o provedor de serviços de hospedagem ou Microsoft Azure, onde o usuário de saudação não é proprietário Olá malha camada.

## <a name="connected-sources"></a>Fontes conectadas

Dados de transmissão obtém seus dados de saudação Microsoft Dependency Agent. Olá Dependency Agent depende de saudação do agente do OMS para sua análise de tooLog de conexões. Isso significa que um servidor deve ter Olá agente do OMS instalado e configurado o primeiro e, em seguida, você pode instalar Olá Dependency Agent. Olá tabela a seguir descreve fontes Olá conectado que dá suporte à solução de dados de transmissão de saudação.

| **Fonte conectada** | **Com suporte** | **Descrição** |
| --- | --- | --- |
| Agentes do Windows | Sim | O Wire Data analisa e coleta dados de computadores de agente do Windows. <br><br> Em adição toohello [agente do OMS](log-analytics-windows-agents.md), agentes do Windows exigem Olá Microsoft Dependency Agent. Consulte Olá [sistemas operacionais com suporte](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) para obter uma lista completa de versões do sistema operacional. |
| Agentes do Linux | Sim | O Wire Data analisa e coleta dados de computadores de agente do Linux.<br><br> Em adição toohello [agente do OMS](log-analytics-linux-agents.md), agentes Linux exigem Olá Microsoft Dependency Agent. Consulte Olá [sistemas operacionais com suporte](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) para obter uma lista completa de versões do sistema operacional. |
| Grupo de gerenciamento do System Center Operations Manager | Sim | O Wire Data analisa e coleta dados de agentes do Windows e do Linux em um [grupo de gerenciamento do System Center Operations Manager](log-analytics-om-agents.md) conectado. <br><br> Uma conexão direta de saudação do System Center Operations Manager agent computador tooLog análise é necessária. Dados são encaminhados de tooLog de grupo de gerenciamento Olá análise. |
| Conta de Armazenamento do Azure | Não | Dados de transmissão coleta dados de computadores de agente, portanto não há nenhum dado dele toocollect do armazenamento do Azure. |

No Windows, Olá agente de monitoramento da Microsoft (MMA) é usado pelo System Center Operations Manager e análise de Log toogather e enviar dados. Dependendo do contexto de Olá, agente de saudação é chamado hello agente do System Center Operations Manager, agente do OMS, o agente de análise de Log, MMA ou agente direto. System Center Operations Manager e análise de Log fornecem ligeiramente diferentes versões do hello MMA. Essas versões de cada relatório tooSystem Center Operations Manager, tooLog análise ou tooboth.

No Linux, Olá agente do OMS para Linux coleta e envia dados tooLog análise. Você pode usar dados de transmissão em servidores com agentes do OMS direta ou em servidores que estão anexado tooLog análise por meio de grupos de gerenciamento do System Center Operations Manager.

Neste artigo, referencia se tooall agentes, Linux ou Windows, se o grupo de gerenciamento do System Center Operations Manager tooa conectado ou diretamente tooLog análise são chamados Olá _agente do OMS_. Usaremos o nome de implantação específica de saudação do agente Olá somente se ela for necessária para o contexto.

Olá Dependency Agent não transmite todos os dados em si, e não requer qualquer toofirewalls alterações ou portas. Olá dados em dados de transmissão é sempre serão transmitidos por Olá OMS agente tooLog Analytics, seja diretamente ou usando Olá Gateway do OMS.

![diagrama do agente](./media/log-analytics-wire-data/agents.png)

Se você for um usuário do System Center Operations Manager com um grupo conectado de gerenciamento tooLog análise:

- Nenhuma configuração adicional é necessária quando os agentes do System Center Operations Manager podem acessar Olá Internet tooconnect tooLog análise.
- Você precisa tooconfigure Olá OMS Gateway toowork com o System Center Operations Manager quando os agentes do System Center Operations Manager não podem acessar a análise de Log pela Olá da Internet.

Se você estiver usando Olá agente direto, você precisará tooconfigure Olá OMS próprio agente tooconnect tooLog análise ou tooyour Gateway do OMS. Você pode baixar Olá Gateway de OMS do hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

## <a name="prerequisites"></a>Pré-requisitos

- Requer Olá [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) oferta da solução.
- Se você estiver usando a versão anterior de saudação do hello solução durante a transmissão de dados, primeiro remova-lo. No entanto, todos os dados capturados por meio da solução de dados de transmissão original Olá ainda está disponível no 2.0 de dados durante a transmissão e pesquisa de log.
- Privilégios de administrador são necessária tooinstall ou desinstale Olá Dependency Agent.
- Olá Dependency Agent deve ser instalado em um computador com um sistema operacional de 64 bits.

### <a name="operating-systems"></a>Sistemas operacionais

Olá seções a seguir listam Olá suporte para sistemas operacionais Olá Dependency Agent. O Wire Data não dá suporte a arquiteturas de 32 bits de nenhum sistema operacional.

#### <a name="windows-server"></a>Windows Server

- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

#### <a name="windows-desktop"></a>Área de trabalho do Windows

- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux e Oracle Linux (com Kernel RHEL)

- Somente as versões de kernel padrão e Linux SMP têm suporte.
- Nenhuma distribuição do Linux dá suporte às versões de kernel não padrão, como PAE e Xen. Por exemplo, um sistema com a cadeia de caracteres de versão de saudação do _2.6.16.21-0.8-xen_ não tem suporte.
- Não há suporte para kernels personalizados, incluindo recompilações de kernels padrão.
- Não há suporte para o kernel CentOSPlus.
- O UEK (Unbreakable Enterprise Kernel) da Oracle é abordado em uma seção posterior deste artigo.

#### <a name="red-hat-linux-7"></a>Red Hat Linux 7

| **Versão do SO** | **Versão do kernel** |
| --- | --- |
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7,2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6

| **Versão do SO** | **Versão do kernel** |
| --- | --- |
| 6,0 | 2.6.32-71 |
| 6.1 | 2.6.32-131 |
| 6.2 | 2.6.32-220 |
| 6.3 | 2.6.32-279 |
| 6.4 | 2.6.32-358 |
| 6.5 | 2.6.32-431 |
| 6.6 | 2.6.32-504 |
| 6.7 | 2.6.32-573 |
| 6,8 | 2.6.32-642 |

#### <a name="red-hat-linux-5"></a>Red Hat Linux 5

| **Versão do SO** | **Versão do kernel** |
| --- | --- |
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398 <br> 2.6.18-400 <br>2.6.18-402 <br>2.6.18-404 <br>2.6.18-406 <br> 2.6.18-407 <br> 2.6.18-408 <br> 2.6.18-409 <br> 2.6.18-410 <br> 2.6.18-411 <br> 2.6.18-412 <br> 2.6.18-416 <br> 2.6.18-417 <br> 2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux com Unbreakable Enterprise Kernel

#### <a name="oracle-linux-6"></a>Oracle Linux 6

| **Versão do SO** | **Versão do kernel** |
| --- | --- |
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4 | Oracle 2.6.39-400 (UEK R2) |
| 6.5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| **Versão do SO** | **Versão do kernel** |
| --- | --- |
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11

| **Versão do SO** | **Versão do kernel** |
| --- | --- |
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10

| **Versão do SO** | **Versão do kernel** |
| --- | --- |
| 10 SP4 | 2.6.16.60 |

#### <a name="dependency-agent-downloads"></a>Downloads do Agente de Dependência

| **Arquivo** | **SO** | **Versão** | **SHA-256** |
| --- | --- | --- | --- |
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |



## <a name="configuration"></a>Configuração

Execute Olá solução de dados de transmissão de saudação etapas tooconfigure para seus espaços de trabalho a seguir.

1. Habilitar a solução de análise de Log de atividade de saudação da saudação [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) ou usando o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).
2. Instale Olá Dependency Agent em cada computador onde você deseja tooget dados. Olá Dependency Agent pode monitorar vizinhos de tooimmediate de conexões, portanto talvez não seja necessário um agente em cada computador.

### <a name="install-hello-dependency-agent-on-windows"></a>Instalar o hello Dependency Agent no Windows

Privilégios de administrador são necessária tooinstall ou desinstalar o agente de saudação.

Olá Dependency Agent é instalado em computadores que executam o Windows por meio de InstallDependencyAgent Windows.exe. Se você executar esse arquivo executável sem opções, ele inicia um assistente que você pode seguir tooinstall interativamente.

Use Olá seguindo as etapas tooinstall Olá Dependency Agent em cada computador que executa o Windows:

1. Instalar Olá agente do OMS usando instruções Olá em [toohello de computadores Windows conectar-se o serviço de análise de Log no Azure](log-analytics-windows-agents.md).
2. Baixar agente do Windows hello usando Olá link na seção anterior hello e, em seguida, executá-lo usando o comando a seguir de saudação: InstallDependencyAgent Windows.exe
3. Execute o agente de Olá Olá Assistente tooinstall.
4. Se Olá Dependency Agent falhar toostart, verifique os logs de saudação para informações de erro detalhadas. Em agentes do Windows, o diretório de log Olá é %Programfiles%\Microsoft dependência agent\logs..

#### <a name="windows-command-line"></a>Linha de comando do Windows

Use opções de saudação tooinstall tabela a seguir em uma linha de comando. toosee uma lista de sinalizadores de instalação hello, execute o instalador de saudação usando Olá /? da seguinte maneira.

InstallDependencyAgent-Windows.exe /?

| **Sinalizador** | **Descrição** |
| --- | --- |
| <code>/?</code> | Obter uma lista de opções de linha de comando hello. |
| <code>/S</code> | Realize uma instalação silenciosa sem solicitações ao usuário. |

Arquivos de saudação agente de dependência do Windows são colocados em C:\Program Files\Microsoft Dependency Agent por padrão.

### <a name="install-hello-dependency-agent-on-linux"></a>Instalar Olá Dependency Agent no Linux

Acesso à raiz é necessário tooinstall ou configurar o agente de saudação.

Olá Dependency Agent é instalado em computadores Linux por meio de InstallDependencyAgent-Linux64.bin, um script de shell com um binário de extração automática. Você pode executar o arquivo hello usando _sh_ ou adicionar executar o próprio arquivo de toohello permissões.

Use Olá seguindo as etapas tooinstall Olá Dependency Agent em cada computador Linux:

1. Instalar Olá agente do OMS usando instruções Olá em [coletar e gerenciar dados de computadores Linux](log-analytics-agent-linux.md).
2. Baixar o agente do Linux dependência hello usando Olá link na seção anterior hello e instalá-lo como raiz usando o comando a seguir de saudação: sh InstallDependencyAgent Linux64.bin
3. Se Olá Dependency Agent falhar toostart, verifique os logs de saudação para informações de erro detalhadas. Agentes do Linux, o diretório de log de saudação:: /var/opt/microsoft/dependency-agent/log.

toosee uma lista de sinalizadores de instalação hello, execute o programa de instalação de saudação com hello `-help` sinalizador da seguinte maneira.

```
InstallDependencyAgent-Linux64.bin -help
```

| **Sinalizador** | **Descrição** |
| --- | --- |
| <code>-help</code> | Obter uma lista de opções de linha de comando hello. |
| <code>-s</code> | Realize uma instalação silenciosa sem solicitações ao usuário. |
| <code>--check</code> | Verifique as permissões e o sistema operacional de saudação, mas não instale o agente de saudação. |

Arquivos de saudação Dependency Agent são colocados em Olá diretórios a seguir:

| **Arquivos** | **Localidade** |
| --- | --- |
| Arquivos de núcleo | /opt/microsoft/dependency-agent |
| Arquivos de log | /var/opt/microsoft/dependency-agent/log |
| Arquivos de configuração | /etc/opt/microsoft/dependency-agent/config |
| Arquivos executáveis de serviço | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br><br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| Arquivos de armazenamento binário | /var/opt/microsoft/dependency-agent/storage |

### <a name="installation-script-examples"></a>Exemplos de script de instalação

tooeasily implantar Olá agente dependência em vários servidores ao mesmo tempo, ele ajuda a toouse um script. Você pode usar o hello toodownload de exemplos de script a seguir e instalar Olá Dependency Agent no Windows ou Linux.

#### <a name="powershell-script-for-windows"></a>Script do PowerShell para Windows

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a>Script de Shell para Linux

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a>Configuração de estado desejado

Olá toodeploy Dependency Agent por meio da configuração de estado desejado, você pode usar o módulo xPSDesiredStateConfiguration de saudação e um trecho de código com hello seguinte:

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install hello Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-hello-dependency-agent"></a>Desinstalar Olá Dependency Agent

Use Olá toohelp seções remover Olá Dependency Agent a seguir.

#### <a name="uninstall-hello-dependency-agent-on-windows"></a>Desinstalar Olá agente de dependência no Windows

Um administrador pode desinstalar Olá dependência de agente do Windows por meio do painel de controle.

Um administrador também pode executar %Programfiles%\Microsoft Agent\Uninstall.exe dependência toouninstall Olá Dependency Agent.

#### <a name="uninstall-hello-dependency-agent-on-linux"></a>Desinstalar Olá agente dependência no Linux

desinstalação toocompletely Olá dependência agente do Linux, remova o próprio agente hello e Olá conector, que é instalado automaticamente com o agente de saudação. Você pode desinstalar usando Olá único comando a seguir:

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a>Pacotes de gerenciamento

Quando dados de transmissão é ativado em um espaço de trabalho de análise de Log, um pacote de gerenciamento de 300 KB é enviado a servidores do Windows hello tooall nesse espaço de trabalho. Se você estiver usando agentes do System Center Operations Manager em um [grupo de gerenciamento conectado](log-analytics-om-agents.md), Olá pacote de gerenciamento do Monitor de dependência é implantado a partir do System Center Operations Manager. Se os agentes de saudação estão diretamente conectados, análise de Log fornece o pacote de gerenciamento Olá.

pacote de gerenciamento de saudação é denominado Microsoft.IntelligencePacks.ApplicationDependencyMonitor. Ele é gravado em: %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs. Olá fonte de dados que usa o pacote de gerenciamento de saudação é: % Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="using-hello-solution"></a>Usando a solução de saudação

**Instalando e configurando a solução Olá**

Use Olá tooinstall informações a seguir e configurar a solução de saudação.

- Olá solução durante a transmissão de dados adquire dados de computadores que executam o Windows Server 2012 R2, Windows 8.1 e sistemas operacionais posteriores.
- Microsoft .NET Framework 4.0 ou posterior é necessário nos computadores onde você deseja que os dados durante a transmissão tooacquire.
- Adicionar Olá dados de transmissão solução tooyour análise de Log espaço de trabalho usando Olá processo descrito na [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md). Não é necessária nenhuma configuração.
- Se você quiser dados de transmissão tooview para uma solução específica, você precisa de solução de saudação toohave já adicionada tooyour espaço de trabalho.

Depois de instalar agentes e instale Olá solução, o bloco de Olá 2.0 de dados durante a transmissão é exibido em seu espaço de trabalho.

> [!NOTE]
> No momento, você deve usar dados de transmissão Olá OMS tooview portal. Você não pode usar dados de transmissão Olá tooview portal do Azure.

![Bloco do Wire Data](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-hello-wire-data-20-solution"></a>Usando a solução Olá 2.0 de dados durante a transmissão

No portal do OMS hello, clique em Olá **2.0 de dados de transmissão** painel de dados de transmissão do bloco tooopen hello. painel Olá inclui folhas Olá Olá a tabela a seguir. Cada folha lista os itens too10 correspondência critérios da folha de saudação especificado escopo e tempo de intervalo. Você pode executar uma pesquisa de log que retorna todos os registros clicando **ver todos os** na parte inferior da folha de saudação ou clicando o cabeçalho de folha de saudação do hello.

| **Folha** | **Descrição** |
| --- | --- |
| Agentes capturando tráfego de rede | Mostra o número de saudação de agentes que está capturando tráfego de rede e lista Olá top 10 computadores que estão capturando o tráfego. Clique em toorun número Olá uma pesquisa de log para <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>. Clique em um computador em Olá lista toorun uma pesquisa de log retornando Olá o número total de bytes capturados. |
| Sub-redes locais | Mostra o número de saudação de sub-redes locais que agentes descobertos.  Clique em toorun número Olá uma pesquisa de log para <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> que lista todas as sub-redes com número de saudação de bytes enviados em cada um deles. Clique em uma sub-rede em Olá lista toorun uma pesquisa de log retornando Olá o número total de bytes enviados pela sub-rede de saudação. |
| Protocolos no nível do aplicativo | Mostra o número de saudação de protocolos de nível de aplicativo em uso, como detectados pelos agentes. Clique em toorun número Olá uma pesquisa de log para <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>. Clique em um protocolo toorun uma pesquisa de log retornando Olá o número total de bytes enviados usando o protocolo de saudação. |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Painel do Wire Data](./media/log-analytics-wire-data/wire-data-dash.png)

Você pode usar o hello **agentes capturando tráfego de rede** toodetermine folha quanta largura de banda de rede está sendo consumida pelos computadores. Esta folha pode ajudá-lo facilmente localizar Olá _chattiest_ computador no seu ambiente. Esses computadores podem estar sobrecarregados, operando de modo anormal ou usando mais recursos de rede que o normal.

![exemplo de pesquisa de logs](./media/log-analytics-wire-data/log-search-example01.png)

Da mesma forma, você pode usar o hello **sub-redes locais** toodetermine folha quanto o tráfego de rede está se movendo por meio de suas sub-redes. Os usuários geralmente definem sub-redes em torno de áreas críticas para seus aplicativos. Esta folha oferece uma exibição dessas áreas.

![exemplo de pesquisa de logs](./media/log-analytics-wire-data/log-search-example02.png)

Olá **protocolos de nível de aplicativo** folha é útil porque é útil saber quais protocolos estão em uso. Por exemplo, você pode esperar SSH toonot estar em uso em seu ambiente de rede. Exibindo informações disponíveis na folha de saudação rapidamente pode confirmar ou conteste suas expectativas.

![exemplo de pesquisa de logs](./media/log-analytics-wire-data/log-search-example03.png)

Neste exemplo, você pode analisar em SSH detalhes toosee quais computadores estão usando SSH e muitos outros detalhes de comunicação.

![resultados da pesquisa sh](./media/log-analytics-wire-data/ssh-details.png)

Também é útil tooknow se o tráfego do protocolo está aumentando ou diminuindo ao longo do tempo. Por exemplo, se estiver aumentando a quantidade de saudação dos dados transmitidos por um aplicativo, que pode ser algo que você deve estar atento, ou que pode ser importante.

## <a name="input-data"></a>Dados de entrada

Dados de transmissão coleta metadados sobre o tráfego de rede usando Olá agentes que você tiver habilitado. Cada agente envia dados aproximadamente a cada 15 segundos.

## <a name="output-data"></a>Dados de saída

Um registro com um tipo de _WireData_ é criado para cada tipo de dados de entrada. Registros de WireData têm propriedades mostradas na Olá a tabela a seguir:

| Propriedade | Descrição |
|---|---|
| Computador | Nome do computador em que os dados foram coletados |
| TimeGenerated | Hora do registro de saudação |
| LocalIP | Endereço IP do computador local Olá |
| SessionState | Conectado ou desconectado |
| ReceivedBytes | Quantidade de bytes recebidos |
| ProtocolName | Nome do protocolo de rede Olá usado |
| IPVersion | Versão IP |
| Direção | Entrada ou saída |
| MaliciousIP | Endereço IP de uma fonte mal-intencionada conhecida |
| Severity | Gravidade de suspeita de malware |
| RemoteIPCountry | País do endereço IP remoto de saudação |
| ManagementGroupName | Nome do grupo de gerenciamento do Operations Manager Olá |
| SourceSystem | Fonte na qual o dados foram coletados |
| SessionStartTime | Hora de início da sessão |
| SessionEndTime | Hora de término da sessão |
| LocalSubnet | Sub-rede na qual o dados foram coletados |
| LocalPortNumber | Número da porta local |
| RemoteIP | Endereço IP remoto usado pelo computador remoto Olá |
| RemotePortNumber | Número da porta usada pelo endereço IP remoto de saudação |
| SessionID | Um valor exclusivo que identifica a sessão de comunicação entre os dois endereços IP |
| SentBytes | Número de bytes enviados |
| TotalBytes | Número total de bytes enviados durante a sessão |
| ApplicationProtocol | Tipo de protocolo de rede usado   |
| ProcessID | ID de processo do Windows |
| ProcessName | Nome de arquivo e caminho do processo de saudação |
| RemoteIPLongitude | Valor de longitude do IP |
| RemoteIPLatitude | Valor de latitude do IP |


## <a name="next-steps"></a>Próximas etapas

- [Pesquisar logs](log-analytics-log-searches.md) tooview detalhadas registros de pesquisa de dados de transmissão.
