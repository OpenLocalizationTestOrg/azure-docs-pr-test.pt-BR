---
title: "alterações de aaaTrack com análise de logs do Azure | Microsoft Docs"
description: "Olá solução de controle de alterações na análise de Log ajuda a identificar o software e alterações de serviço do Windows que ocorrem em seu ambiente."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f8040d5d-3c89-4f0c-8520-751c00251cb7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2bb1938caad25101e167927200ac3ef495120fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="track-software-changes-in-your-environment-with-hello-change-tracking-solution"></a>Controlar as alterações de software em seu ambiente com hello solução controle de alterações

![Símbolo do Controle de Alterações](./media/log-analytics-change-tracking/change-tracking-symbol.png)

Este artigo ajuda você a use Olá solução de controle de alterações na análise de Log tooeasily identificar alterações em seu ambiente. solução de saudação rastreia alterações tooWindows e software Linux, arquivos do Windows e chaves do registro, serviços do Windows e Linux daemons. Identificar as alterações de configuração pode ajudá-lo a detectar problemas operacionais.

Instalar o tipo de saudação do hello solução tooupdate de agente que você instalou. Alterações tooinstalled software, serviços do Windows e daemons do Linux em servidores de saudação monitorada são lidos. Olá os dados são enviados de serviço de análise de Log toohello na nuvem Olá para processamento. Lógica é aplicada toohello recebida dados e o serviço de nuvem Olá registra dados de saudação. Usando informações de saudação no painel de controle de alterações de saudação, você pode ver facilmente as alterações de saudação que foram feitas em sua infraestrutura de servidor.

## <a name="installing-and-configuring-hello-solution"></a>Instalando e configurando a solução Olá
Use Olá tooinstall informações a seguir e configurar a solução de saudação.

* Você deve ter uma [Windows](log-analytics-windows-agents.md), [Operations Manager](log-analytics-om-agents.md), ou [Linux](log-analytics-linux-agents.md) agente em cada computador em que você deseja toomonitor alterações.
* Adicionar Olá Change Tracking solução tooyour OMS espaço de trabalho de saudação [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ChangeTrackingOMS?tab=Overview). Ou, você pode adicionar solução hello usando informações Olá [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md). Nenhuma configuração adicional é necessária.

### <a name="configure-linux-files-tootrack"></a>Configurar tootrack de arquivos Linux
Use Olá seguindo as etapas tooconfigure arquivos tootrack em computadores Linux.

1. No portal do OMS hello, clique em **configurações** (símbolo de engrenagem Olá).
2. Em Olá **configurações** , clique em **dados**e, em seguida, clique em **controle de arquivo do Linux**.
3. Em controle de alterações do arquivo de Linux, digite o caminho inteiro hello, incluindo nome do arquivo de saudação do arquivo hello que você deseja tootrack e, em seguida, clique em Olá **adicionar** símbolo. Por exemplo: “/etc/*.conf”
4. Clique em **Salvar**.  

> [!NOTE]
> O controle de arquivos do Linux tem funcionalidades adicionais, incluindo controle de diretórios, recursão por diretórios e controle de curingas.

### <a name="configure-windows-files-tootrack"></a>Configurar tootrack de arquivos do Windows
Use Olá seguindo as etapas tooconfigure arquivos tootrack em computadores Windows.

1. No portal do OMS hello, clique em **configurações** (símbolo de engrenagem Olá).
2. Em Olá **configurações** , clique em **dados**e, em seguida, clique em **controle de arquivo do Windows**.
3. Em controle de alterações do arquivo de Windows, digite o caminho inteiro hello, incluindo nome do arquivo de saudação do arquivo hello que você deseja tootrack e, em seguida, clique em Olá **adicionar** símbolo. Por exemplo: C:\Program Files (x86)\Internet Explorer\iexplore.exe ou C:\Windows\System32\drivers\etc\hosts.
4. Clique em **Salvar**.  
   ![Controle de Alterações de Arquivo do Windows](./media/log-analytics-change-tracking/windows-file-change-tracking.png)

### <a name="configure-windows-registry-keys-tootrack"></a>Configurar tootrack de chaves de registro do Windows
Use Olá tootrack de chaves de registro de tooconfigure as etapas a seguir em computadores Windows.

1. No portal do OMS hello, clique em **configurações** (símbolo de engrenagem Olá).
2. Em Olá **configurações** , clique em **dados**e, em seguida, clique em **controle de registro do Windows**.
3. Em controle de alterações de registro de Windows, digite Olá toda a chave que você deseja tootrack e, em seguida, clique em Olá **adicionar** símbolo.
4. Clique em **Salvar**.  
   ![Controle de alterações de Registro de Windows](./media/log-analytics-change-tracking/windows-registry-change-tracking.png)

### <a name="explanation-of-linux-file-collection-properties"></a>Explicação das propriedades da coleção de arquivos do Linux
1. **Tipo**
   * **Arquivo** (relate os metadados do arquivo – tamanho, data de modificação, hash, etc.)
   * **Diretório** (relate os metadados do diretório – tamanho, data de modificação, etc.)
2. **Links** (Linux tratamento symlink referencia tooother arquivos ou diretórios)
   * **Ignorar** (links simbólicos de ignorar durante recurions toonot incluem hello arquivos/diretórios referenciados)
   * **Execute** (seguir links simbólicos de saudação durante recursão tooalso incluem hello arquivos/diretórios referenciados)
   * **Gerenciar** (siga os links simbólicos do hello e alterar o tratamento de saudação do conteúdo retornado)

   > [!NOTE]   
   > não é recomendável Hello "Gerenciar" opção de links. Não há suporte para a recuperação de conteúdo do arquivo.

3. **Recurse** (Recurse por níveis de pasta e acompanhar todos os arquivos que correspondem a instrução de caminho Olá)
4. **Sudo** (habilite o acesso a arquivos ou diretórios que exigem privilégios do sudo)

### <a name="limitations"></a>Limitações
Olá solução controle de alterações não oferece suporte a saudação itens a seguir:

* Pastas (diretórios) para o Controle de Arquivos do Windows
* Recursão para o Controle de Arquivos do Windows
* Curingas para o Controle de Arquivos do Windows
* Variáveis de caminho
* Sistemas de arquivos de rede
* Conteúdo do arquivo

Outras limitações:

* Olá **tamanho máximo de arquivo** coluna e valores são usados na implementação atual de saudação.
* Se você coletar arquivos de mais de 2500 no ciclo de coleta de 30 minutos de saudação, o desempenho da solução pode ser degradado.
* Quando o tráfego de rede for alto, registros de alteração podem levar até tooa máximo de seis horas toodisplay.
* Se você modificar a configuração de saudação enquanto um computador é desligado, computador Olá pode lançar alterações no arquivo pertenciam a configuração anterior toohello.

## <a name="change-tracking-data-collection-details"></a>Detalhes de coleta de dados do Controle de Alterações
Controle de alterações coleta de inventário de software e metadados de serviço do Windows usando Olá agentes que você tiver habilitado.

Olá tabela a seguir mostra os métodos de coleta de dados e outros detalhes sobre como os dados são coletados para o controle de alterações.

| plataforma | Agente direto | Agente do Operations Manager | Agente do Linux | Armazenamento do Azure | Operations Manager necessário? | Dados de agente do Operations Manager enviados por meio do grupo de gerenciamento | frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Windows e Linux | &#8226; | &#8226; | &#8226; |  |  | &#8226; | 5 minutos too50 minutos, dependendo do tipo de alteração de saudação. Consulte Olá tabela para obter mais informações a seguir. |


Olá tabela a seguir mostra frequência de coleta de dados Olá para tipos de saudação de alterações.

| **change type** | **frequency** | **O** **agente** **envia as diferenças quando encontradas?**  |
| --- | --- | --- |
| Registro do Windows | 50 minutos | Não |
| Arquivo do Windows | 30 minutos | Sim. Se não houver nenhuma alteração em até 24 horas, um instantâneo é enviado. |
| Arquivo Linux | 15 minutos | Sim. Se não houver nenhuma alteração em até 24 horas, um instantâneo é enviado. |
| Serviços do Windows | 30 minutos | Sim, quando as alterações são encontradas a cada 30 minutos. A cada 24 horas um instantâneo é enviado, independentemente da mudança. Portanto, instantâneo Olá é enviado até mesmo quando não há nenhuma alteração. |
| Daemons Linux | 5 minutos | Sim. Se não houver nenhuma alteração em até 24 horas, um instantâneo é enviado. |
| Software do Windows | 30 minutos | Sim, quando as alterações são encontradas a cada 30 minutos. A cada 24 horas um instantâneo é enviado, independentemente da mudança. Portanto, instantâneo Olá é enviado até mesmo quando não há nenhuma alteração. |
| Software Linux | 5 minutos | Sim. Se não houver nenhuma alteração em até 24 horas, um instantâneo é enviado. |

### <a name="registry-key-change-tracking"></a>Controle de alterações de chave do Registro

Análise de log executa monitoramento e rastreamento com hello solução controle de alterações de registro do Windows. finalidade de saudação do monitoramento de alterações tooregistry chaves é toopinpoint pontos de extensibilidade onde o código de terceiros e malware podem ativar. lista a seguir de saudação chaves mostra saudação padrão do registro que são controlados pela solução hello e por que cada um é rastreada.

- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Startup
    - Monitora scripts que são executados na inicialização.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Shutdown
    - Monitora scripts que são executados no desligamento.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run
    - Monitora as chaves que são carregadas antes Olá usuário se autentica no tootheir conta do Windows. Olá chave é usada para programas de 32 bits em execução em computadores de 64 bits.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Active Setup\Installed Components
    - Monitora as alterações tooapplication configurações.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\ShellEx\ContextMenuHandlers
    - Monitores entradas comuns de inicialização automática que se conectam diretamente ao Windows Explorer e geralmente são executadas no processo com o Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Shellex\CopyHookHandlers
    - Monitores entradas comuns de inicialização automática que se conectam diretamente ao Windows Explorer e geralmente são executadas no processo com o Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Background\ShellEx\ContextMenuHandlers
    - Monitores entradas comuns de inicialização automática que se conectam diretamente ao Windows Explorer e geralmente são executadas no processo com o Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Monitora o registro do manipulador de sobreposição de ícone.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Monitora o registro do manipulador de sobreposição de ícone para programas de 32 bits executados em computadores de 64 bits.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
    - Monitora os novos plug-ins de objeto auxiliar de navegador para o Internet Explorer. Tooaccess usados Olá DOM Document Object Model () de navegação atual de página e toocontrol hello.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
    - Monitora os novos plug-ins de objeto auxiliar de navegador para o Internet Explorer. Tooaccess usados Olá DOM Document Object Model () do hello página e toocontrol navegação atual para programas de 32 bits em execução em computadores de 64 bits.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Internet Explorer\Extensions
    - Monitora novas extensões do Internet Explorer, tais como menus de ferramentas personalizadas e botões da barra de ferramentas personalizada.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Internet Explorer\Extensions
    - Monitora novas extensões do Internet Explorer, como menus de ferramentas personalizadas e botões de barra de ferramentas personalizada para programas de 32 bits executados em computadores de 64 bits.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Monitora os drivers de 32 bits Olá associados wavemapper, wave1 e wave2, msacm.imaadpcm, .msadpcm, .msgsm610 e vidc. Seção toohello [drivers] semelhante Olá sistema. Arquivo INI.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Drivers de 32 bits Olá monitores associados wavemapper, wave1 e wave2, msacm.imaadpcm, .msadpcm, .msgsm610 e vidc para programas de 32 bits em execução em computadores de 64 bits. Seção toohello [drivers] semelhante Olá sistema. Arquivo INI.
- HKEY\_LOCAL\_MACHINE\System\CurrentControlSet\Control\Session Manager\KnownDlls
    - Monitores Olá lista conhecido ou usada das DLLs do sistema; Este sistema impede que pessoas explorando permissões de diretório de aplicativo fraca soltando em cavalo de Troia versões de DLLs do sistema.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify
    - Monitores Olá lista pacotes tooreceive capaz de notificações de eventos do Winlogon, o modelo de suporte de logon interativo Olá para o sistema de operacional do Windows hello.


## <a name="use-change-tracking"></a>Use o Controle de Alterações
Depois Olá solução estiver instalada, você pode exibir o resumo de saudação de alterações para os servidores monitorados usando Olá **Change Tracking** bloco Olá **visão geral** página no OMS.

![imagem de bloco Controle de Alterações](./media/log-analytics-change-tracking/change-tracking-tile.png)

Você pode exibir as alterações tooyour infraestrutura e então analisar em detalhes para Olá categorias a seguir:

* Alterações por tipo de configuração para serviços de software e do Windows
* Alterações de software tooapplications e atualizações para servidores individuais
* Número total de alterações de software para cada aplicativo
* Pacotes do Linux
* Alterações no serviço Windows para servidores individuais
* Alterações de daemon do Linux

![imagem do painel Controle de Alterações](./media/log-analytics-change-tracking/change-tracking-dash01.png)

![imagem do painel Controle de Alterações](./media/log-analytics-change-tracking/change-tracking-dash02.png)

### <a name="tooview-changes-for-any-change-type"></a>alterações de tooview para qualquer tipo de alterações
1. Em Olá **visão geral** , clique em Olá **Change Tracking** lado a lado.
2. Em Olá **Change Tracking** painel, examine as informações de resumo de saudação em uma das folhas de tipo de alteração de saudação e, em seguida, clique em uma tooview informações detalhadas sobre ele no hello **pesquisa de log** página.
3. Em qualquer uma das páginas de pesquisa de log hello, você pode exibir os resultados por tempo, resultados detalhados e o histórico de pesquisa de log. Você também pode filtrar pelos resultados de saudação toonarrow facetas.

## <a name="next-steps"></a>Próximas etapas
* Use [pesquisas de Log na análise de Log](log-analytics-log-searches.md) tooview obter dados de controle de alterações.
