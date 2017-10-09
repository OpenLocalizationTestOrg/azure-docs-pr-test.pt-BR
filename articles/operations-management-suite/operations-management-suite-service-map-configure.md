---
title: "aaaConfigure mapa de serviço no Operations Management Suite | Microsoft Docs"
description: "Mapa de serviço é uma solução Operations Management Suite que detecta automaticamente os componentes do aplicativo no Windows e mapas e sistemas Linux Olá comunicação entre serviços. Este artigo fornece detalhes sobre a implantação do Mapa do Serviço em seu ambiente e sobre como usá-lo em diversos cenários."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: d3d66b45-9874-4aad-9c00-124734944b2e
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/18/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: 3127f4440f2886370f8ff617c405c6d70a926eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-service-map-in-operations-management-suite"></a>Configurar o Mapa do Serviço no Operations Management Suite
Mapa de serviço detecta automaticamente os componentes do aplicativo em sistemas Windows e Linux e mapas Olá comunicação entre serviços. Você pode usá-lo tooview os servidores que você imagina — como sistemas interconectados que fornecem serviços essenciais. O Mapa do Serviço mostra conexões entre servidores, processos e portas em qualquer arquitetura conectada a TCP sem nenhuma configuração necessária além da instalação de um agente.

Este artigo descreve os detalhes de saudação de configuração de agentes de mapa de serviço e integração. Para obter informações sobre como usar o mapa de serviço, consulte [usar solução de mapa de serviço de saudação do Operations Management Suite](operations-management-suite-service-map.md).

## <a name="dependency-agent-downloads"></a>Downloads do Agente de Dependência
| Arquivo | SO | Versão | SHA-256 |
|:--|:--|:--|:--|
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |


## <a name="connected-sources"></a>Fontes conectadas
Mapa de serviço obtém seus dados de saudação Microsoft Dependency Agent. Olá Dependency Agent depende de saudação do agente do OMS para suas conexões de tooOperations Management Suite. Isso significa que um servidor deve ter Olá agente do OMS instalado e configurado primeiro e, em seguida, Olá que dependência agente pode ser instalado. Olá tabela a seguir descreve fontes de saudação conectada Olá solução de mapa de serviço oferece suporte.

| Fonte conectada | Suportado | Descrição |
|:--|:--|:--|
| Agentes do Windows | Sim | O Mapa do Serviço analisa e coleta dados de computadores de agente do Windows. <br><br>Em adição toohello [agente do OMS](../log-analytics/log-analytics-windows-agents.md), agentes do Windows exigem Olá Microsoft Dependency Agent. Consulte Olá [sistemas operacionais com suporte](#supported-operating-systems) para obter uma lista completa de versões do sistema operacional. |
| Agentes do Linux | Sim | O Mapa do Serviço analisa e coleta dados de computadores de agente do Linux. <br><br>Em adição toohello [agente do OMS](../log-analytics/log-analytics-linux-agents.md), agentes Linux exigem Olá Microsoft Dependency Agent. Consulte Olá [sistemas operacionais com suporte](#supported-operating-systems) para obter uma lista completa de versões do sistema operacional. |
| Grupo de gerenciamento do System Center Operations Manager | Sim | O Mapa do Serviço analisa e coleta dados de agentes do Windows e do Linux em um [grupo de gerenciamento do System Center Operations Manager](../log-analytics/log-analytics-om-agents.md) conectado. <br><br>Uma conexão direta de saudação do System Center Operations Manager agent computador tooOperations Management Suite é necessário. Dados são encaminhados do repositório de Operations Management Suite toohello do grupo de gerenciamento de saudação.|
| Conta de Armazenamento do Azure | Não | Mapa de serviço coleta dados de computadores de agente, portanto não há nenhum dado dele toocollect do armazenamento do Azure. |

O Mapa do Serviço só dá suporte a plataformas de 64 bits.

No Windows, Olá agente de monitoramento da Microsoft (MMA) é usado pelo System Center Operations Manager e o Operations Management Suite toogather e enviar dados de monitoramento. (Esse agente é chamado hello agente do System Center Operations Manager, agente do OMS, o agente de análise de Log, MMA ou agente direto, dependendo do contexto de saudação). System Center Operations Manager e o Operations Management Suite fornecem versões de caixa de saída de hello diferente do hello MMA. Essas versões de cada relatório tooSystem Center Operations Manager, tooOperations Management Suite ou tooboth.  

No Linux, hello agente do OMS para Linux coleta e envia dados tooOperations pacote de gerenciamento de monitoramento. Você pode usar o mapa de serviço em servidores com agentes do OMS direta ou em servidores que estão anexados tooOperations Management Suite por meio de grupos de gerenciamento do System Center Operations Manager.  

Neste artigo, vamos nos referir agentes tooall – se Linux ou Windows, se conectado grupo de gerenciamento do System Center Operations Manager tooa ou diretamente tooOperations Management Suite – como hello "Agente do OMS". Usaremos o nome de implantação específica de saudação do agente Olá somente se ela for necessária para o contexto.

Agente de mapa de serviço Olá não transmite todos os dados em si, e não requer qualquer toofirewalls alterações ou portas. dados de Olá no mapa de serviço sempre são transmitidos por Olá tooOperations do agente do OMS Management Suite, diretamente ou por meio de saudação do OMS Gateway.

![Agentes do Mapa do Serviço](media/oms-service-map/agents.png)

Se você for um cliente do System Center Operations Manager com um grupo conectado de gerenciamento tooOperations Management Suite:

- Se os agentes do System Center Operations Manager podem acessar Olá Internet tooconnect tooOperations Management Suite, nenhuma configuração adicional é necessária.  
- Se os agentes do System Center Operations Manager não podem acessar o Operations Management Suite pela Olá da Internet, será necessário tooconfigure Olá OMS Gateway toowork com o System Center Operations Manager.
  
Se você estiver usando Olá agente direto do OMS, você precisará tooconfigure Olá próprio agente de OMS tooconnect tooOperations Management Suite ou tooyour Gateway do OMS. Olá OMS Gateway pode ser baixado do hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

### <a name="management-packs"></a>Pacotes de gerenciamento
Quando o mapa de serviço é ativado em um espaço de trabalho do Operations Management Suite, um pacote de gerenciamento de 300 KB é enviado a servidores do Windows hello tooall nesse espaço de trabalho. Se você estiver usando agentes do System Center Operations Manager em um [grupo de gerenciamento conectado](../log-analytics/log-analytics-om-agents.md), Olá pacote de gerenciamento do mapa de serviço é implantado a partir do System Center Operations Manager. Se os agentes de saudação estão diretamente conectados, Operations Management Suite fornece o pacote de gerenciamento hello.

pacote de gerenciamento de saudação é denominado Microsoft.IntelligencePacks.ApplicationDependencyMonitor. É escrito too%Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs\. fonte de dados que usa o pacote de gerenciamento Olá Olá é % Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources\<AutoGeneratedID > \ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="installation"></a>Instalação
### <a name="install-hello-dependency-agent-on-microsoft-windows"></a>Instalar Olá Dependency Agent no Microsoft Windows
Privilégios de administrador são necessária tooinstall ou desinstalar o agente de saudação.

Olá Dependency Agent é instalado em computadores com Windows por meio de InstallDependencyAgent Windows.exe. Se você executar esse arquivo executável sem opções, ele inicia um assistente que você pode seguir tooinstall interativamente.  

Use Olá seguindo as etapas tooinstall Olá Dependency Agent em cada computador com Windows:

1.  Instalar Olá agente do OMS usando instruções Olá em [toohello de computadores Windows conectar-se o serviço de análise de Log no Azure](../log-analytics/log-analytics-windows-agents.md).
2.  Baixe o agente do Windows hello e executá-lo usando o comando a seguir de saudação: <br>`InstallDependencyAgent-Windows.exe`
3.  Execute o agente de Olá Olá Assistente tooinstall.
4.  Se Olá Dependency Agent falhar toostart, verifique os logs de saudação para informações de erro detalhadas. Em agentes do Windows, o diretório de log Olá é %Programfiles%\Microsoft dependência agent\logs.. 

#### <a name="windows-command-line"></a>Linha de comando do Windows
Use opções de saudação tooinstall tabela a seguir em uma linha de comando. toosee uma lista de sinalizadores de instalação hello, execute o instalador de saudação usando Olá /? da seguinte maneira.

    InstallDependencyAgent-Windows.exe /?

| Sinalizador | Descrição |
|:--|:--|
| /? | Obter uma lista de opções de linha de comando hello. |
| /S | Realize uma instalação silenciosa sem solicitações ao usuário. |

Arquivos de saudação agente de dependência do Windows são colocados em C:\Program Files\Microsoft Dependency Agent por padrão.

### <a name="install-hello-dependency-agent-on-linux"></a>Instalar Olá Dependency Agent no Linux
Acesso à raiz é necessário tooinstall ou configurar o agente de saudação.

Olá Dependency Agent é instalado em computadores Linux por meio de InstallDependencyAgent-Linux64.bin, um script de shell com um binário de extração automática. Você pode executar o arquivo hello usando sh ou adicionar executar o próprio arquivo de toohello permissões.
 
Use Olá seguindo as etapas tooinstall Olá Dependency Agent em cada computador Linux:

1.  Instalar Olá agente do OMS usando instruções Olá em [coletar e gerenciar dados de computadores Linux](https://technet.microsoft.com/library/mt622052.aspx).
2.  Instale o agente de dependência do Linux do hello como raiz usando Olá comando a seguir:<br>`sh InstallDependencyAgent-Linux64.bin`
3.  Se Olá Dependency Agent falhar toostart, verifique os logs de saudação para informações de erro detalhadas. Agentes do Linux, o diretório de log Olá é /var/opt/microsoft/dependency-agent/log.

toosee uma lista de sinalizadores de instalação hello, execute o programa de instalação de saudação com hello - sinalizador de Ajuda da seguinte maneira.

    InstallDependencyAgent-Linux64.bin -help

| Sinalizador | Descrição |
|:--|:--|
| -help | Obter uma lista de opções de linha de comando hello. |
| -s | Realize uma instalação silenciosa sem solicitações ao usuário. |
| --check | Verifique as permissões e o sistema operacional de saudação, mas não instale o agente de saudação. |

Arquivos de saudação Dependency Agent são colocados em Olá diretórios a seguir:

| Arquivos | Local |
|:--|:--|
| Arquivos de núcleo | /opt/microsoft/dependency-agent |
| Arquivos de log | /var/opt/microsoft/dependency-agent/log |
| Arquivos de configuração | /etc/opt/microsoft/dependency-agent/config |
| Arquivos executáveis de serviço | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| Arquivos de armazenamento binário | /var/opt/microsoft/dependency-agent/storage |

## <a name="installation-script-examples"></a>Exemplos de script de instalação
tooeasily implantar Olá agente dependência em vários servidores ao mesmo tempo, ele ajuda a toouse um script. Você pode usar o hello toodownload de exemplos de script a seguir e instalar Olá Dependency Agent no Windows ou Linux.

### <a name="powershell-script-for-windows"></a>Script do PowerShell para Windows
```PowerShell
Invoke-WebRequest "https://aka.ms/dependencyagentwindows" -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S
```

### <a name="shell-script-for-linux"></a>Script de Shell para Linux
```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
sh InstallDependencyAgent-Linux64.bin -s
```

## <a name="desired-state-configuration"></a>Configuração de estado desejado
Olá toodeploy Dependency Agent por meio da configuração de estado desejado, você pode usar o módulo xPSDesiredStateConfiguration de saudação e um trecho de código com hello seguinte:
```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install hello Dependency Agent
    xRemoteFile DAPackage 
    {
        Uri = "https://aka.ms/dependencyagentwindows"
        DestinationPath = $DAPackageLocalPath
    }

    xPackage DA
    {
        Ensure="Present"
        Name = "Dependency Agent"
        Path = $DAPackageLocalPath
        Arguments = '/S'
        ProductId = ""
        InstalledCheckRegKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent"
        InstalledCheckRegValueName = "DisplayName"
        InstalledCheckRegValueData = "Dependency Agent"
        DependsOn = "[xRemoteFile]DAPackage"
    }
  }
}
```

## <a name="uninstallation"></a>Desinstalação
### <a name="uninstall-hello-dependency-agent-on-windows"></a>Desinstalar Olá agente de dependência no Windows
Um administrador pode desinstalar Olá dependência de agente do Windows por meio do painel de controle.

Um administrador também pode executar %Programfiles%\Microsoft Agent\Uninstall.exe dependência toouninstall Olá Dependency Agent.

### <a name="uninstall-hello-dependency-agent-on-linux"></a>Desinstalar Olá agente dependência no Linux
desinstalação toocompletely Olá dependência agente do Linux, remova o próprio agente hello e Olá conector, que é instalado automaticamente com o agente de saudação. Você pode desinstalar usando Olá único comando a seguir:

    rpm -e dependency-agent dependency-agent-connector

## <a name="troubleshooting"></a>Solucionar problemas
Se você enfrentar problemas ao instalar ou executar o Mapa do Serviço, esta seção poderá lhe ajudar. Se ainda não for possível resolver o problema, entre em contato com o Suporte da Microsoft.

### <a name="dependency-agent-installation-problems"></a>Problemas de instalação do Agente de Dependência
#### <a name="installer-asks-for-a-reboot"></a>O instalador solicita uma reinicialização
Olá Dependency Agent *geralmente* não requer uma reinicialização após a instalação ou desinstalação. No entanto, em alguns casos raros, o Windows Server requer toocontinue uma reinicialização com uma instalação. Isso ocorre quando uma dependência, geralmente Olá Microsoft Visual C++ redistribuível, requer uma reinicialização devido a um arquivo bloqueado.

#### <a name="message-unable-tooinstall-dependency-agent-visual-studio-runtime-libraries-failed-tooinstall-code--codenumber-appears"></a>Mensagem "não é possível tooinstall Dependency Agent: bibliotecas de tempo de execução do Visual Studio Falha tooinstall (código = [code_number])" é exibida

Olá Microsoft Dependency Agent é criado em bibliotecas de tempo de execução do Microsoft Visual Studio hello. Se houver um problema durante a instalação das bibliotecas de saudação, você receberá uma mensagem. 

instaladores de biblioteca de tempo de execução Olá criar logs na pasta de %LOCALAPPDATA%\temp hello. arquivo Hello é dd_vcredist_arch_yyyymmddhhmmss.log, onde *arch* é "x86" ou "amd64" e *yyyymmddhhmmss* date de hello e a hora (formato de 24 horas) em que o log de saudação foi criado. log Olá fornece detalhes sobre o problema de saudação que está bloqueando a instalação.

Talvez seja útil tooinstall Olá [bibliotecas de tempo de execução mais recentes](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) por conta própria primeiro.

Olá tabela a seguir lista os números de código e soluções sugeridas.

| Código | Descrição | Resolução |
|:--|:--|:--|
| 0x17 | instalador de biblioteca Olá requer uma atualização do Windows que não foi instalada. | Procure no log de instalador de biblioteca mais recente hello.<br><br>Se uma referência muito "Windows8.1-KB2999226-x64" é seguido por uma linha de "Erro 0x80240017: pacote MSU tooexecute com falha," hello pré-requisitos tooinstall KB2999226 não é necessário. Siga as instruções de saudação na seção pré-requisitos Olá [Universal C Runtime no Windows](https://support.microsoft.com/kb/2999226). Você pode precisar toorun Windows Update e reiniciado várias vezes nos pré-requisitos do pedido tooinstall hello.<br><br>Execute o instalador do Microsoft Dependency Agent Olá novamente. |

### <a name="post-installation-issues"></a>Problemas pós-instalação
#### <a name="server-doesnt-appear-in-service-map"></a>O servidor não aparece no Mapa do Serviço
Se a instalação do agente de dependência foi bem-sucedida, mas você não vir o servidor em Olá solução Mapa de serviço:
* Olá Dependency Agent é instalado com êxito? Você pode validar isso verificando toosee se Olá serviço está instalado e em execução.<br><br>
**Windows**: procure Olá serviço chamado "Microsoft Dependency agente".<br>
**Linux**: procure Olá executando o processo "microsoft-dependência-agente".

* Você está no hello [livre preço Operations Management Suite/da análise de Log](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)? plano gratuito Olá permite que os servidores de mapa de serviço exclusivos toofive. Quaisquer servidores subsequentes serão exibidos no mapa de serviço, mesmo se Olá cinco anterior não estão enviando dados.

* É o envio de log do servidor e dados de desempenho tooOperations Management Suite? TooLog pesquisar e executar Olá consulta para o seu computador a seguir: 

        * Computer="<your computer name here>" | measure count() by Type
        
  Você obteve uma variedade de eventos nos resultados de Olá? Dados de saudação é recente? Nesse caso, o agente do OMS está operando corretamente e se comunicando com hello serviço Operations Management Suite. Caso contrário, verifique a saudação do agente do OMS em seu servidor: [solução de problemas de agente do OMS para Windows](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues) ou [agente do OMS para Linux de solução de problemas](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md).

#### <a name="server-appears-in-service-map-but-has-no-processes"></a>O servidor aparece no Mapa do Serviço, mas sem processos
Se você ver o servidor no mapa de serviço, mas nenhum dado de processo ou de conexão, que indica que Olá Dependency Agent está instalado e em execução, mas o driver de kernel Olá não foi carregado. 

Verifique o arquivo de C:\Program Files\Microsoft dependência Agent\logs\wrapper.log hello (Windows) ou /var/opt/microsoft/dependency-agent/log/service.log (Linux). últimas linhas de saudação do arquivo hello devem indicar por que o kernel Olá não foi carregado. Por exemplo, kernel Olá talvez não tenha suporte Linux se você atualizou o kernel.

## <a name="data-collection"></a>Coleta de dados
Você pode esperar tootransmit cada agente aproximadamente 25 MB por dia, dependendo de como complexas são de suas dependências de sistema. Os dados de dependência do Mapa do Serviço são enviados por cada agente a cada 15 segundos.  

Olá Dependency Agent geralmente consome 0,1 por cento da memória do sistema e 0,1 por cento da CPU do sistema.

## <a name="supported-azure-regions"></a>Regiões do Azure com suporte
Mapa de serviço está disponível em Olá regiões do Azure a seguir:
- Leste dos EUA
- Europa Ocidental
- Centro-Oeste dos EUA


## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte
Olá seções a seguir listam Olá suporte para sistemas operacionais Olá Dependency Agent. O Mapa do Serviço não dá suporte a arquiteturas de 32 bits de nenhum sistema operacional.

### <a name="windows-server"></a>Windows Server
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

### <a name="windows-desktop"></a>Área de trabalho do Windows
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux e Oracle Linux (com Kernel RHEL)
- Somente as versões de kernel padrão e Linux SMP têm suporte.
- Nenhuma distribuição do Linux dá suporte às versões de kernel não padrão, como PAE e Xen. Por exemplo, não há suporte para um sistema com a cadeia de caracteres de versão de saudação do "2.6.16.21-0.8-xen".
- Não há suporte para kernels personalizados, incluindo recompilações de kernels padrão.
- Não há suporte para o kernel CentOSPlus.
- O UEK (Unbreakable Enterprise Kernel) da Oracle é abordado em uma seção posterior deste artigo.


#### <a name="red-hat-linux-7"></a>Red Hat Linux 7
| Versão do SO | Versão do kernel |
|:--|:--|
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7,2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6
| Versão do SO | Versão do kernel |
|:--|:--|
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
| Versão do SO | Versão do kernel |
|:--|:--|
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398<br>2.6.18-400<br>2.6.18-402<br>2.6.18-404<br>2.6.18-406<br>2.6.18-407<br>2.6.18-408<br>2.6.18-409<br>2.6.18-410<br>2.6.18-411<br>2.6.18-412<br>2.6.18-416<br>2.6.18-417<br>2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux com Unbreakable Enterprise Kernel

#### <a name="oracle-linux-6"></a>Oracle Linux 6
| Versão do SO | Versão do kernel
|:--|:--|
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4 | Oracle 2.6.39-400 (UEK R2) |
| 6.5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| Versão do SO | Versão do kernel
|:--|:--|
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11
| Versão do SO | Versão do kernel
|:--|:--|
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10
| Versão do SO | Versão do kernel
|:--|:--|
| 10 SP4 | 2.6.16.60 |

## <a name="diagnostic-and-usage-data"></a>Dados de uso e de diagnóstico
A Microsoft coleta automaticamente dados de uso e desempenho por meio do hello serviço mapa de serviço. A Microsoft usa esse tooprovide de dados e melhorar a qualidade do hello, segurança e integridade de saudação serviço mapa de serviço. Os dados incluem informações sobre a configuração de saudação do software, como o sistema operacional e versão. Ele também inclui o endereço IP, o nome DNS e o nome da estação de trabalho em ordem tooprovide precisas e eficientes para solução de problemas recursos. Não coletamos nomes, endereços ou outras informações de contato.

Para obter mais informações sobre o uso e coleta de dados, consulte Olá [declaração de privacidade do Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=512132).



## <a name="next-steps"></a>Próximas etapas
- Saiba como muito[usar o mapa de serviço](operations-management-suite-service-map.md) depois que ele foi implantado e configurado.
