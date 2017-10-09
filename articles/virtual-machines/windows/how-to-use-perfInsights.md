---
title: aaaHow toouse PerfInsights no Microsoft Azure | Microsoft Docs
description: Aprende como problemas de desempenho do toouse PerfInsights tootroubleshoot VM do Windows.
services: virtual-machines-windows'
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: genli
ms.openlocfilehash: f23ff7708c0c63bd02674b1bdc07753e8a89d9be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-perfinsights"></a>Como toouse PerfInsights 

[PerfInsights](http://aka.ms/perfinsightsdownload) é um script automatizado que coleta informações de diagnósticas úteis, executa as cargas de estresse de e/s e fornece um toohelp do relatório de análise solucionar problemas de desempenho de VM do Windows no Microsoft Azure. 

É recomendável executar esse script antes de abrir um chamado de suporte com a Microsoft para problemas de desempenho da VM.

## <a name="supported-troubleshooting-scenarios"></a>Cenários de solução de problemas com suporte

O PerfInsights pode coletar e analisar vários tipos de informações que são agrupadas em cenários exclusivos.

### <a name="collect-disk-configuration"></a>Coletar configuração de disco 

Este cenário coleta a configuração de disco hello e outras informações importantes, incluindo Olá itens a seguir:

-   Logs de eventos

-   Status da rede para todas as conexões de entrada e saída

-   Definições de configuração de firewall e rede

-   Lista de tarefas para todos os aplicativos que estão sendo executados no sistema de saudação

-   Arquivo de informações criado pelo msinfo32 para Olá VM (máquina virtual)

-   Definições de configuração do banco de dados do Microsoft SQL Server (se Olá VM é identificado como um servidor que executa o SQL Server)

-   Contadores de confiabilidade do armazenamento

-   Hotfixes importantes do Windows

-   Drivers de filtro instalados

Esta é uma coleção de passiva de informações que não devem afetar o sistema hello. 

>[!Note]
>Este cenário é incluído automaticamente em cada um dos seguintes cenários de saudação.

### <a name="benchmarkstorage-performance-test"></a>Teste de desempenho de armazenamento/parâmetro de comparação

Este cenário é executado Olá [diskspd](https://github.com/Microsoft/diskspd) avaliar o desempenho de teste (IOPS e MBPS) para todas as unidades que são anexadas toohello VM. 

> [!Note]
> Esse cenário pode afetar o sistema hello e não deve ser executado em um sistema de produção. Se necessário, execute este cenário em um tooavoid da janela de manutenção dedicada quaisquer problemas. Uma carga de trabalho maior é causada por um teste de rastreamento ou parâmetro de comparação pode afetar adversamente o desempenho de saudação da VM.
>

### <a name="general-vm-slow-analysis"></a>Análise geral de VM lenta 

Este cenário é executada uma [contador de desempenho](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) rastreamento usando os contadores de saudação que são especificados no arquivo de Generalcounters.txt hello. Se hello VM for identificada como um servidor que executa o SQL Server, ele é executado um rastreamento de contador de desempenho usando contadores de saudação que são encontrados no arquivo de Sqlcounters.txt hello. Também inclui dados de Diagnóstico de Desempenho.

### <a name="vm-slow-analysis-and-benchmark"></a>Parâmetro de comparação e análise de VM lenta

Este cenário executa um rastreamento do [contador de desempenho](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) que é seguido pelo teste de parâmetro de comparação [diskspd](https://github.com/Microsoft/diskspd). 

> [!Note]
> Esse cenário pode afetar o sistema hello e não deve ser executado em um sistema de produção. Se necessário, execute este cenário em um tooavoid da janela de manutenção dedicada quaisquer problemas. Uma carga de trabalho maior é causada por um teste de rastreamento ou parâmetro de comparação pode afetar adversamente o desempenho de saudação da VM.
>

### <a name="azure-files-analysis"></a>Análise de Arquivos do Azure 

Este cenário executa uma captura de contador de desempenho especial junto com um rastreamento de rede. A captura inclui todos os contadores de "Compartilhamentos de cliente SMB" hello. Olá seguem alguns chave SMB cliente compartilhamento contadores de desempenho que fazem parte da captura de saudação:

| **Tipo**     | **Contador de compartilhamentos de cliente SMB** |
|--------------|-------------------------------|
| IOPS         | Solicitações de dados/s             |
|              | Solicitações de leitura/s             |
|              | Solicitações de gravação/s            |
| Latência      | Solicitação de dados/s média         |
|              | Média de leituras/s                 |
|              | Média de s/gravação                |
| Tamanho de E/S      | Média Bytes/solicitação de dados       |
|              | Média Bytes/leitura               |
|              | Média Bytes/gravação              |
| Taxa de transferência   | Bytes de dados/s                |
|              | Bytes de leitura/s                |
|              | Bytes de gravação/s               |
| Comprimento da fila | Média Tamanho da fila de leitura        |
|              | Média Tamanho da fila de gravação       |
|              | Média Comprimento da fila de dados        |

### <a name="custom-configuration"></a>Configuração personalizada 

Quando você executa uma configuração personalizada, está executando todos os rastreamentos (diagnóstico de desempenho, contador de desempenho, xperf, rede, storport) em paralelo, dependendo de quantos rastreamentos diferentes são selecionados. Após o rastreamento, ferramenta Olá executa Olá diskspd de parâmetro de comparação se estiver selecionada. 

> [!Note]
> Esse cenário pode afetar o sistema hello e não deve ser executado em um sistema de produção. Se necessário, execute este cenário em um tooavoid da janela de manutenção dedicada quaisquer problemas. Uma carga de trabalho maior é causada por um teste de rastreamento ou parâmetro de comparação pode afetar adversamente o desempenho de saudação da VM.
>

## <a name="what-kind-of-information-is-collected-by-hello-script"></a>Que tipo de informações é coletado pelo script hello?

Configuração de pools de informações sobre a máquina virtual do Windows, discos ou armazenamento, contadores de desempenho, logs e vários rastreamentos são coletados dependendo do cenário de desempenho Olá usado:

|Dados coletados                              |  |  | Cenários de desempenho |  |  | |
|----------------------------------|----------------------------|------------------------------------|--------------------------|--------------------------------|----------------------|----------------------|
|                              | Coletar Configuração de Disco | Teste de desempenho de armazenamento/parâmetro de comparação | Análise geral de VM lenta | Parâmetro de comparação e análise de VM lenta | Análise de Arquivos do Azure | Configuração personalizada |
| Informações de logs de eventos      | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Informações do sistema               | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Mapa de volume                       | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Mapa do disco                         | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Tarefas em execução                    | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Contadores de Confiabilidade do Armazenamento     | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Informações de armazenamento              | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Saída do fsutil                    | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Informações do driver de filtro               | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Saída de Netstat                   | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Configuração de rede            | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Configuração do firewall           | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Configuração do SQL Server         | Sim                        | Sim                                | Sim                      | Sim                            | Sim                  | Sim                  |
| Rastreamentos de diagnóstico de desempenho * |                            |                                    | Sim                      |                                |                      | Sim                  |
| Rastreamento do contador de desempenho **     |                            |                                    |                          |                                |                      | Sim                  |
| Rastreamento do contador SMB **             |                            |                                    |                          |                                | Sim                  |                      |
| Rastreamento do contador do SQL Server **      |                            |                                    |                          |                                |                      | Sim                  |
| Rastreamento de XPerf                      |                            |                                    |                          |                                |                      | Sim                  |
| Rastreamento de StorPort                   |                            |                                    |                          |                                |                      | Sim                  |
| Rastreamento de rede                    |                            |                                    |                          |                                | Sim                  | Sim                  |
| Rastreamento de parâmetro de comparação de Diskspd ***      |                            | Sim                                |                          | Sim                            |                      |                      |
|       |                            |                         |                                                   |                      |                      |

### <a name="performance-diagnostics-trace-"></a>Rastreamento de diagnóstico de desempenho (*)

Executa um mecanismo de regra nos dados de toocollect do plano de fundo hello e diagnosticar problemas de desempenho em andamento. Olá regras a seguir é atualmente suportado:

- Regra de HighCpuUsage: detecta longos períodos de uso de CPU e mostra os principais consumidores de uso de CPU Olá durante esses períodos.
- Regra de HighDiskUsage: detecta os períodos de uso alto de disco em discos físicos e mostra os consumidores de uso de disco superior Olá durante esses períodos.
- Regra de HighResolutionDiskMetric: mostra IOPS, taxa de transferência e métricas de latência de E/S por 50 milissegundos para cada disco físico. Ele ajuda a tooquickly identificar períodos de limitação de disco.
- Regra de HighMemoryUsage: detecta os períodos de uso de memória alta e mostra os consumidores de uso de memória superior Olá durante esses períodos.

> [!NOTE] 
> Atualmente, as versões do Windows que incluem a saudação do .NET Framework 3.5 ou versões posteriores têm suporte.

### <a name="performance-counter-trace-"></a>Rastreamento do contador de desempenho (**)

Saudação de coleta contadores de desempenho a seguir:

- \Process, \Processor, \Memory, \Thread, \PhysicalDisk, \LogicalDisk
- \Cache\Dirty Pages, \Cache\Lazy Write Flushes/sec, \Server\Pool Nonpaged, Failures, \Server\Pool Paged Failures
- Contadores selecionados em \Network Interface, \IPv4\Datagrams, \IPv6\Datagrams, \TCPv4\Segments, \TCPv6\Segments,  \Network Adapter, \WFPv4\Packets, \WFPv6\Packets, \UDPv4\Datagrams, \UDPv6\Datagrams, \TCPv4\Connection, \TCPv6\Connection, \Network QoS Policy\Packets, \Per Processor Network Interface Card Activity, \Microsoft Winsock BSP

#### <a name="for-sql-server-instances"></a>Para instâncias do SQL Server
- \SQL Server:Buffer Manager, \SQLServer:Resource Pool Stats, \SQLServer:SQL Statistics\
- \SQLServer:Locks, \SQLServer:General, Statistics
- \SQLServer:Access Methods

#### <a name="for-azure-files"></a>Para Arquivos do Azure
\SMB Client Shares

### <a name="diskspd-benchmark-trace-"></a>Rastreamento de parâmetro de comparação de Diskspd (***)
Testes de carga de trabalho de E/S do Diskspd [disco do SO (gravação) e unidades de pool (leitura/gravação)]

## <a name="run-hello-perfinsights-on-your-vm"></a>Executar Olá PerfInsights na sua VM

### <a name="what-do-i-have-tooknow-before-i-run-hello-script"></a>O que é necessário tooknow antes de executar script hello? 

**Requisitos de script**

1.  Esse script deve ser executado em Olá VM que tem um problema de desempenho de saudação. 

2.  Olá OSes seguir têm suporte: Windows Server 2008 R2, 2012, 2012 R2, 2016; Windows 8.1 e Windows 10.

**Possíveis problemas quando você executa o script hello em produção VMs:**

1.  script Hello pode afetar negativamente o desempenho de saudação do hello VM quando ela é usada junto com o cenário de "Parâmetro de comparação" ou "Custom" hello configurado usando XPerf ou DiskSpd. Tenha cuidado ao executar o script hello em um ambiente de produção.

2.  Quando você usa o script hello junto com o cenário de "Parâmetro de comparação" ou "Custom" hello que é configurado usando o DiskSpd, certifique-se de que nenhuma outra atividade de plano de fundo interfere com carga de trabalho de e/s de saudação em discos Olá testado.

3.  Por padrão, o script hello usa dados de toocollect de unidade de armazenamento temporário de saudação. Se o rastreamento permaneça habilitada por mais tempo, quantidade Olá dos dados coletados pode ser relevante. Isso pode reduzir a disponibilidade de saudação do espaço em disco temporário do hello, afetando, portanto, qualquer aplicativo que depende dessa unidade.

### <a name="how-do-i-run-perfinsights"></a>Como fazer para executar o PerfInsights? 

toorun Olá script, siga estas etapas:

1. Baixe [PerfInsights.zip](http://aka.ms/perfinsightsdownload).

2. Desbloquear o arquivo de PerfInsights.zip hello. toodo isso, o arquivo de PerfInsights.zip de saudação com o botão direito, selecione **propriedades**. Em Olá **geral** guia, selecione **desbloquear** e, em seguida, selecione **Okey**. Isso irá assegurar que o script hello é executado sem prompts de segurança adicional.  

    ![Desbloquear o arquivo zip de saudação](media/how-to-use-perfInsights/unlock-file.png)

3.  Expanda Olá compactado PerfInsights.zip arquivo na unidade temporária (por padrão, geralmente a unidade Olá D). Olá arquivo compactado deve conter Olá seguinte arquivos e pastas:

    ![arquivos na pasta de zip Olá](media/how-to-use-perfInsights/file-folder.png)

4.  Abra o Windows PowerShell como administrador e, em seguida, execute o script de PerfInsights.ps1 de saudação.

    ```
    cd <hello path of PerfInsights folder >
    Powershell.exe -ExecutionPolicy UnRestricted -NoProfile -File .\\PerfInsights.ps1
    ```

    Você pode ter tooenter "y" tooif tiver solicitado tooconfirm que você deseja toochange política de execução de saudação.

    Na caixa de diálogo de aviso de isenção de saudação, você terá Olá opção tooshare informações de diagnóstico com a Microsoft Support. Você também deve consentir toohello toocontinue de contrato de licença. Faça suas seleções e, em seguida, clique em **Executar Script**.

    ![Caixa de diálogo Aviso de Isenção de Responsabilidade](media/how-to-use-perfInsights/disclaimer.png)

5.  Envie o número do caso hello, se ele estiver disponível, ao executar o script hello (Isso é para nosso estatísticas). Em seguida, clique em **OK**.
    
    ![inserir ID de suporte](media/how-to-use-perfInsights/enter-support-number.png)

6.  Selecione a unidade de armazenamento temporário. Olá Script pode detectar automaticamente letra Olá da unidade de saudação. Se houver problemas neste estágio, você pode ser solicitado a unidade de saudação tooselect (a unidade padrão de saudação é D). Os logs gerados são armazenados aqui no log de saudação\_pasta da coleção. Depois que você insira ou aceite a letra da unidade hello, clique em **Okey**.

    ![inerir unidade](media/how-to-use-perfInsights/enter-drive.png)

7.  Selecione um cenário de solução de problemas da saudação lista.

       ![Selecionar cenários de suporte](media/how-to-use-perfInsights/select-scenarios.png)

8.  Você também pode executar PerfInsights sem interface do usuário.

    seguir Olá Olá execuções de comando "Análise de geral lenta de VM" cenário sem um prompt de interface do usuário de solução de problemas ou captura dados de 30 segundos. Solicita tooconsent toohello mesmo isenção de responsabilidade e EULA mencionados na etapa 4.

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30"

    Se você quiser PerfInsights toorun no modo silencioso, use o **- AcceptDisclaimerAndShareDiagnostics** parâmetro. Por exemplo, use Olá comando a seguir:

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30 -AcceptDisclaimerAndShareDiagnostics"

### <a name="how-do-i-troubleshoot-issues-while-running-hello-script"></a>Como solucionar os problemas durante a execução do script hello?

Se o script hello terminado de maneira anormal, é possível limpar um estado inconsistente, executando o script hello junto com hello - comutador de limpeza, da seguinte maneira:

    powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -Cleanup"

Se houver problemas durante a detecção automática de unidade temporária Olá Olá, talvez seja solicitado a unidade de saudação tooselect (a unidade padrão de saudação é D).

![enter-drive](media/how-to-use-perfInsights/enter-drive.png)

script Hello desinstala ferramentas de utilitários hello e remove as pastas temporárias.

### <a name="troubleshooting-other-script-issues"></a>Solução de outros problemas de script 

Se houver problemas ao executar o script hello, pressione Ctrl + C execução do script de saudação do toointerrupt. tooremove de objetos temporários, consulte a seção de "Limpeza após o encerramento anormal" hello.

Se você continuar a falha do script tooexperience mesmo após várias tentativas, é recomendável que você execute o script hello no "modo de depuração" usando hello "-Debug" opção de parâmetro na inicialização.

Depois de falha de saudação ocorre, cópia Olá completo saída do console do PowerShell Olá e envie-o agente do Microsoft Support toohello que está ajudando você toohelp solucionar problema de saudação.

### <a name="how-do-i-run-hello-script-in-custom-configuration-mode"></a>Como executar o script hello no modo de configuração personalizado?

Selecionando Olá **personalizado** configuração, você pode habilitar vários rastreamentos em paralelo (use Shift toomulti-selecione):

![selecionar cenários](media/how-to-use-perfInsights/select-scenario.png)

Quando você seleciona Olá diagnóstico de desempenho, rastreamento de contador de desempenho, XPerf rastreamento, rastreamento de rede ou cenários de rastreamento Storport, siga as instruções de Olá Olá caixas de diálogo e tente a problemas de desempenho lento Olá tooreproduce depois que você inicie os rastreamentos de saudação.

Olá, caixa de diálogo a seguir permite que você iniciar um rastreamento:

![start-trace](media/how-to-use-perfInsights/start-trace-message.png)

rastreamentos, a saudação toostop tiver tooconfirm comando de saudação em uma segunda caixa de diálogo.

![stop-trace](media/how-to-use-perfInsights/stop-trace-message.png)
![stop-trace](media/how-to-use-perfInsights/ok-trace-message.png)

Quando Olá rastreamentos ou operações serem concluídas, um novo arquivo é gerado em d:\\log\_coleção (ou unidade temporária Olá) nomeada **CollectedData\_AAAA-MM-dd\_hh\_mm \_ss.zip.** Você pode enviar o agente de suporte de toohello esse arquivo para análise.

## <a name="review-hello-diagnostics-report-created-by-perfinsights"></a>Examine o relatório de diagnóstico de saudação criado pelo PerfInsights

Dentro de saudação **CollectedData\_AAAA-MM-dd\_hh\_mm\_ss.zip arquivo,** que é gerado pelo PerfInsights, você pode localizar um relatório HTML que fornece detalhes sobre as descobertas de saudação do PerfInsights. tooreview Olá relatório, expanda Olá **CollectedData\_AAAA-MM-dd\_hh\_mm\_ss.zip** de arquivo e abra Olá **PerfInsights Report.html**arquivo.

Selecione Olá **descobertas** guia.

![guia localizar](media/how-to-use-perfInsights/findingtab.png)

**Observações**

-   Mensagens em vermelho são problemas de configuração conhecidos que podem causar problemas de desempenho.

-   Mensagens em amarelo são avisos que representam configurações não ideais que não necessariamente causam problemas de desempenho.

-   As mensagens em azul são somente instruções informativas.

Saudação de revisão links HTTP para todas as mensagens de erro em vermelho tooget mais informações detalhadas sobre descobertas hello e como eles podem afetar o desempenho de saudação ou práticas recomendadas para configurações de otimização de desempenho.

### <a name="disk-configuration-tab"></a>Guia Configuração de Disco

Olá **visão geral** seção exibe os diferentes modos de exibição da configuração de armazenamento de hello, incluindo informações de Diskpart e espaços de armazenamento

Olá **DiskMap** e **VolumeMap** seções descrevem em uma perspectiva dupla lógica como volumes e discos físicos são relacionada tooeach outros.

Olá PhysicalDisk perspectiva (DiskMap), tabela Olá mostra todos os volumes lógicos que estão em execução no disco hello. Saudação de exemplo a seguir, PhysicalDrive2 é executada 2 Volumes lógicos criado em várias partições (J e H):

![guia dados](media/how-to-use-perfInsights/disktab.png)

Em Olá perspectiva de Volume (*VolumeMap*), tabelas de saudação mostram todos os discos físicos de saudação em cada volume lógico. Observe que, para discos RAID/Dinâmicos, você pode executar um volume lógico em vários discos físicos. Em Olá exemplo a seguir *c:\\montar* é configurado como um ponto de montagem *SpannedDisk* na PhysicalDisks \#2 e \#3:

![Guia de volume](media/how-to-use-perfInsights/volumetab.png)

### <a name="sql-server-tab"></a>Guia SQL Server

Se a VM de destino Olá hospeda todas as instâncias do SQL Server, você verá uma guia adicional no relatório Olá denominado **do SQL Server**:

![guia sql](media/how-to-use-perfInsights/sqltab.png)

Esta seção contém uma visão "geral" e guias sub adicionais para cada uma das instâncias do SQL Server Olá hospedadas em Olá VM.

Olá seção "Visão geral" contém uma tabela útil que resume todos os Olá discos físicos (discos de sistema e dados) que estão em execução e que contêm uma mistura de arquivos de dados e arquivos de log de transações.

Em Olá seguinte exemplo, *PhysicalDrive0* (executando a unidade C do hello) é exibida porque ambos Olá *modeldev* e *modellog* arquivos estão localizados na unidade C do hello, e elas são de tipos diferentes (como arquivo de dados e Log de transações, respectivamente):

![loginfo](media/how-to-use-perfInsights/loginfo.png)

guias de específicos da instância do SQL Server Olá contêm uma seção geral que exibe informações básicas sobre a instância selecionada do hello e seções adicionais para obter informações avançadas, incluindo configurações, as configurações e opções do usuário.

## <a name="references-toohello-external-tools-used"></a>Faz referência a toohello ferramentas externas usadas

### <a name="diskspd"></a>Diskspd

DISKSPD é uma carga gerador e desempenho teste ferramenta armazenamento das equipes de engenharia Windows e Windows Server e infraestrutura de servidor de nuvem hello. Para obter mais informações, consulte [Diskspd](https://github.com/Microsoft/diskspd).

### <a name="xperf"></a>XPerf

XPerf é rastreamentos de toocapture uma ferramenta de linha de comando do hello Kit de ferramentas de desempenho do Windows.

Para obter mais informações, consulte [Windows Performance Toolkit – Xperf](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/).

## <a name="next-steps"></a>Próximas etapas

### <a name="upload-diagnostics-logs-and-reports-toomicrosoft-support-for-further-review"></a>Carregar logs de diagnóstico e relatórios tooMicrosoft suporte para análise

Quando você trabalha com hello da equipe do Microsoft Support, pode ser saída de hello tootransmit solicitada que é gerada pelo PerfInsights tooassist Olá Solucionando problemas do processo.

o agente de suporte Olá criará um espaço de trabalho DTM para você, e você receberá uma mensagem de email que inclui um toohello link [DTM portal (https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm) e uma ID exclusiva de usuário e senha.

Esta mensagem será enviada de **Serviços de Diagnóstico Automatizados CTS** (ctsadiag@microsoft.com).

![Exemplo de mensagem de saudação](media/how-to-use-perfInsights/supportemail.png)

Para obter segurança adicional, será necessário toochange sua senha no primeiro usar.

Depois de efetuar login tooDTM, você encontrará uma saudação de tooupload de caixa de diálogo **CollectedData\_AAAA-MM-dd\_hh\_mm\_ss.zip** arquivo foi coletado por PerfInsights.
