---
title: "aaaDebugging um Azure serviço de nuvem ou máquina virtual no Visual Studio | Microsoft Docs"
description: "Depuração de um Serviço de Nuvem ou Máquina Virtual no Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 945e06e0-2100-41af-b218-72347367ddab
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 32a326430021ba2ea9317a6a71fa005d4b87c273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-an-azure-cloud-service-or-virtual-machine-in-visual-studio"></a>Depurando um serviço de nuvem ou máquina virtual do Azure no Visual Studio
O Visual Studio oferece a você opções diferentes de depuração dos serviços de nuvem e das máquinas virtuais do Azure.

## <a name="debug-your-cloud-service-on-your-local-computer"></a>Depurar o serviço de nuvem no computador local
Você pode economizar tempo e dinheiro usando toodebug de emulador de computação do Azure Olá seu serviço de nuvem em um computador local. Ao depurar um serviço localmente antes de implantá-lo, você pode aprimorar a confiabilidade e o desempenho sem pagar pelo tempo de computação. No entanto, alguns erros podem ocorrer somente quando você executa um serviço de nuvem no Azure em si. Se você habilitar a depuração remota quando você publica o serviço e, em seguida, anexar a instância de função hello depurador tooa, você pode depurar esses erros.

emulador de saudação simula o serviço de computação do Azure hello e é executado no ambiente local para que você possa testar e depurar seu serviço de nuvem antes de implantá-lo. identificadores de emulador Olá Olá ciclo de vida de suas instâncias de função e fornece acesso toosimulated recursos, como o armazenamento local. Quando você depura ou executar o serviço do Visual Studio, ela automaticamente inicia o emulador hello como um aplicativo de plano de fundo e implanta o emulador do serviço de toohello. Você pode usar Olá emulador tooview seu serviço quando ele é executado no ambiente local hello. Você pode executar Olá completo versão ou Olá expressa do emulador hello. (Começando com 2.3 do Azure, versão expressa de saudação do emulador Olá é padrão hello.) Consulte [tooRun usando o Emulator Express e depurar um serviço de nuvem localmente](https://msdn.microsoft.com/library/dn339018.aspx).

### <a name="toodebug-your-cloud-service-on-your-local-computer"></a>toodebug sua nuvem de serviço no computador local
1. Na barra de menus do hello, escolha **depurar**, **iniciar depuração** toorun seu projeto de serviço de nuvem do Azure. Como alternativa, você pode pressionar F5. Você verá uma mensagem que Olá Compute Emulator está iniciando. Quando o emulador de saudação é iniciado, ícone de bandeja do sistema Olá confirma isso.

    ![Emulador do Azure na bandeja do sistema Olá](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC783828.png)
2. Exibir a interface do usuário de saudação para o emulador de computação Olá abrindo o menu de atalho Olá para hello Azure ícone na área de notificação hello e, em seguida, selecione **Mostrar UI do emulador de computação**.

    painel esquerdo de saudação do hello da interface do usuário mostra serviços Olá que estão atualmente implantado toohello compute emulator e hello instâncias de função que cada serviço está em execução. Você pode escolher Olá serviços ou funções toodisplay ciclo de vida, o log e informações de diagnóstico no painel direito da saudação. Se você colocar o foco de saudação na margem superior de saudação de uma janela incluída, ele expande o painel direito de saudação toofill.
3. Percorrer aplicativo hello selecionando comandos no hello **depurar** menu e definindo pontos de interrupção no seu código. Como percorrer o aplicativo hello no depurador Olá, painéis Olá são atualizados com o status atual de saudação do aplicativo hello. Quando você interrompe a depuração, implantação de aplicativo hello é excluída. Se seu aplicativo inclui uma função web e que você definiu Olá inicialização ação propriedade toostart Olá navegador, o Visual Studio inicia o aplicativo da web no navegador de saudação. Se você alterar o número de saudação de instâncias de uma função na configuração do serviço Olá, você deve parar o serviço de nuvem e reinicie a depuração de modo que você pode depurar essas novas instâncias de função hello.

    **Observação:** quando você parar de executar ou depurar seu serviço, Olá emulador de computação local e o emulador de armazenamento não são interrompidos. Você deve interrompê-los explicitamente Olá da área de notificação.

## <a name="debug-a-cloud-service-in-azure"></a>Depurar um perfil de serviço de nuvem no Azure
toodebug um serviço de nuvem de um computador remoto, você deve habilitar essa funcionalidade explicitamente quando você implantar seu serviço de nuvem para que o necessário (por exemplo, msvsmon.exe) de serviços estão instalados em máquinas virtuais Olá que executam as instâncias de função. Se você não habilitar a depuração remota quando você publicou serviço hello, você tem serviço de saudação toorepublish com a depuração remota habilitada.

Se você habilitar a depuração remota para um serviço de nuvem, ela não mostrará degradação de desempenho nem incorrerá em cobranças adicionais. Você não deve usar a depuração remota em um serviço de produção, pois os clientes que usam o serviço de saudação podem ser afetados negativamente.

> [!NOTE]
> Quando você publica um serviço de nuvem do Visual Studio, você pode habilitar **IntelliTrace** para funções em que serviço que Olá de destino do .NET Framework 4 ou Olá .NET Framework 4.5. Usando **IntelliTrace**, você pode examinar os eventos que ocorreram em uma instância de função hello anterior e reproduza o contexto de saudação do tempo. Consulte [Depurando um serviço de nuvem publicado com o IntelliTrace e o Visual Studio](http://go.microsoft.com/fwlink/?LinkID=623016) e [Usando o IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx).
>
>

### <a name="tooenable-remote-debugging-for-a-cloud-service"></a>tooenable remota de depuração para um serviço de nuvem
1. Abrir menu de atalho Olá para Olá projeto do Azure e, em seguida, selecione **publicar**.
2. Selecione Olá **preparo** ambiente e hello **depurar** configuração.

    Isso é apenas uma diretriz. Você pode aceitar toorun seus ambientes de teste em um ambiente de produção. No entanto, você pode afetar negativamente os usuários se você habilitar a depuração remota no ambiente de produção de hello. Você pode escolher a configuração de versão de hello, mas torna a configuração de depuração Olá depuração mais fácil.

    ![Escolha a configuração de depuração Olá](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746717.gif)
3. Siga as etapas usuais hello, mas selecione Olá **habilitar depurador remoto para todas as funções** caixa de seleção Olá **configurações avançadas** guia.

    ![Configuração de Depuração](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746718.gif)

### <a name="tooattach-hello-debugger-tooa-cloud-service-in-azure"></a>serviço de nuvem tooattach Olá depurador tooa no Azure
1. No Gerenciador de servidores, expanda o nó de saudação para seu serviço de nuvem.
2. Menu de atalho Olá aberto para a função hello ou toowhich de instância de função você deseja tooattach e, em seguida, selecione **Anexar depurador**.

    Se você depurar uma função, o depurador do Visual Studio Olá anexa tooeach instância dessa função. Olá depurador será interrompido em um ponto de interrupção para Olá primeira instância de função que executa essa linha de código e atende a quaisquer condições de ponto de interrupção. Se você depurar uma instância, o depurador Olá anexa tooonly que a instância e quebras de um ponto de interrupção somente quando aquela instância específica executa essa linha de código e atende Olá condições de ponto de interrupção.

    ![Anexar Depurador](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746719.gif)
3. Depois que o depurador Olá anexa tooan instância, a depuração normalmente. Olá anexado automaticamente toohello o processo de host apropriado para sua função. Dependendo de quais Olá função é, Olá depurador anexa toow3wp.exe, WaWorkerHost.exe ou WaIISHost.exe. tooverify Olá processo toowhich Olá depurador estiver anexado, expanda o nó da instância Olá no Gerenciador de servidores. Consulte [Arquitetura de função do Azure](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx) para obter mais informações sobre os processos do Azure.

    ![Caixa de diálogo Selecionar tipo de código](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
4. processos de saudação tooidentify toowhich Olá depurador é anexado, abrir a caixa de diálogo de processos hello, em Olá barra de menus, escolha Depurar, Windows, processos. (Teclado: Ctrl + Alt + Z) toodetach um processo específico, abra o menu de atalho e, em seguida, selecione **desanexar processo**. Ou, localize o nó da instância Olá no Gerenciador de servidores, encontrar processo hello, abra o menu de atalho e, em seguida, selecione **desanexar processo**.

    ![Processos de depuração](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC690787.gif)

> [!WARNING]
> Evite paradas longas em pontos de interrupção durante a depuração remota. Azure trata um processo que foi interrompido por mais de alguns minutos como sem resposta e interromperá o envio de instância de toothat de tráfego. Se você parar por muito tempo, msvsmon.exe desconecta do processo de saudação.
>
>

depurador de saudação toodetach de todos os processos em sua instância ou a função, o menu de atalho Olá aberto para a função hello ou a instância que você está depurando e, em seguida, selecione **desanexar depurador**.

## <a name="limitations-of-remote-debugging-in-azure"></a>Limitações da depuração remota no Azure
Do SDK 2.3 do Azure, a depuração remota tem Olá limitações a seguir.

* Com a depuração remota habilitada, você não pode publicar um serviço de nuvem no qual qualquer função tenha mais de 25 instâncias.
* depurador Olá usa too30424 30400 portas, 31400 too31424 e too32424 32400. Se você tentar toouse qualquer uma dessas portas, não será capaz de toopublish seu serviço e uma das seguintes mensagens de erro de saudação serão exibida no log de atividades de saudação do Azure:

  * Erro ao validar arquivo. cscfg de saudação em arquivo. csdef de saudação.
    Olá reservado 'intervalo' intervalo de portas para Microsoft.WindowsAzure.Plugins.RemoteDebugger.Connector da função 'função' se sobrepõe a uma porta já definida ou intervalo do ponto de extremidade.
  * Falha na alocação. Tente novamente mais tarde, tente reduzir Olá tamanho da VM ou o número de instâncias de função ou tente implantar tooa uma região diferente.

## <a name="debugging-azure-virtual-machines"></a>Depurando máquinas virtuais do Azure
Você pode depurar programas que são executados em máquinas virtuais do Azure usando o Gerenciador de Servidores no Visual Studio. Quando você habilita a depuração remota em uma máquina virtual do Azure, Azure instala a extensão de depuração remota Olá na máquina virtual de saudação. Em seguida, você pode anexar tooprocesses na máquina virtual de saudação e depurar como faria normalmente.

> [!NOTE]
> Máquinas virtuais criadas por meio da pilha de Gerenciador de recursos do Azure Olá podem ser depuradas remotamente usando o Pesquisador de objetos de nuvem no Visual Studio 2015. Para saber mais, consulte [Gerenciando recursos do Azure com o Cloud Explorer](http://go.microsoft.com/fwlink/?LinkId=623031).
>
>

### <a name="toodebug-an-azure-virtual-machine"></a>toodebug uma máquina virtual do Azure
1. No Gerenciador de servidores, expanda Olá máquinas virtuais nó e selecione Olá da máquina virtual de saudação que você deseja toodebug.
2. Abra o menu de contexto hello e selecione **Ativar depuração**. Quando perguntado se você tem certeza de que se você quiser tooenable depuração na máquina de virtual hello, selecione **Sim**.

    Azure instala a extensão de depuração remota Olá Olá máquina virtual tooenable depuração.

    ![Comando Depuração habilitada para máquina virtual](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Log de atividades do Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
3. Após a extensão de depuração remota Olá concluir a instalação, abra o menu de contexto da máquina de virtual hello e selecione **Anexar depurador...**

    O Azure obtém uma lista de processos de saudação na máquina virtual de saudação e mostra-los na caixa de diálogo de tooProcess Olá anexar.

    ![Comando Anexar depurador](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
4. Em Olá **Attach tooProcess** caixa de diálogo, selecione **selecione** tooshow somente tipos de saudação de lista de resultados de saudação toolimit de código que você deseja toodebug. Você pode depurar um código gerenciado de 32 ou 64 bits, código nativo ou ambos.

    ![Caixa de diálogo Selecionar tipo de código](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
5. Selecione processos Olá você deseja toodebug na máquina virtual de saudação e, em seguida, selecione **Attach**. Por exemplo, você pode escolher processo w3wp.exe de saudação se você desejava toodebug um aplicativo web na máquina virtual de saudação. Consulte [Depurar um ou mais processos no Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) e [Arquitetura de função do Azure](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx) para obter mais informações.

## <a name="create-a-web-project-and-a-virtual-machine-for-debugging"></a>Criar um projeto da Web e uma máquina virtual para depuração
Antes de publicar seu projeto do Azure, talvez você ache útil tootest-lo em um ambiente independente que oferece suporte à depuração e cenários de teste, e onde você pode instalar testes e programas de monitoramento. Toodo unidirecional trata tooremotely depurar seu aplicativo em uma máquina virtual.

Projetos do Visual Studio ASP.NET oferecem uma opção toocreate uma máquina virtual útil que você pode usar para teste de aplicativo. máquina virtual de saudação inclui pontos de extremidade normalmente necessários, como o PowerShell, área de trabalho remota e WebDeploy.

### <a name="toocreate-a-web-project-and-a-virtual-machine-for-debugging"></a>toocreate um projeto da web e uma máquina virtual para depuração
1. No Visual Studio, crie um novo aplicativo Web do ASP.NET.
2. No diálogo do novo projeto ASP.NET hello, em Olá seção do Azure, escolha **Máquina Virtual** na caixa de listagem suspensa hello. Deixe Olá **criar recursos remotos** caixa de seleção. Selecione **Okey** tooproceed.

    Olá **criar a máquina virtual no Azure** caixa de diálogo é exibida.

    ![Caixa de diálogo Criar projeto da Web do ASP.NET](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746723.png)

    **Observação:** deverá toosign em tooyour conta do Azure se você ainda não tiver entrado.

1. Selecione Olá várias configurações para a máquina virtual de saudação e, em seguida, selecione **Okey**. Consulte [Máquinas Virtuais](http://go.microsoft.com/fwlink/?LinkId=623033) para obter mais informações.

    Olá nome para o nome DNS será o nome de saudação da máquina virtual de saudação.

    ![Caixa de diálogo Criar máquina virtual no Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746724.png)

    O Azure cria Olá de máquina virtual e, em seguida, provisiona e configura pontos de extremidade hello, como área de trabalho remota e implantação da Web
2. Depois de saudação máquina virtual está totalmente configurada, selecione o nó de saudação máquina virtual no Gerenciador de servidores.
3. Abra o menu de contexto hello e selecione **Ativar depuração**. Quando perguntado se você tem certeza de que se você quiser tooenable depuração na máquina de virtual hello, selecione **Sim**.

    Azure instala Olá depuração extensão toohello máquina virtual tooenable depuração remota.

    ![Comando Depuração habilitada para máquina virtual](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Log de atividades do Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
4. Publique seu projeto, como descrito em [Como implantar um projeto Web usando a publicação de um clique no Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx). Como você deseja toodebug na máquina virtual de hello, em hello **configurações** página de saudação **Publicar Web** assistente, selecione **depurar** como configuração de saudação. Isso garante que os símbolos de código estejam disponíveis durante a depuração.

    ![Configurações de publicação](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718349.png)
5. Em Olá **opções de publicação do arquivo**, selecione **remover arquivos adicionais no destino** se projeto Olá já foi implantado em um momento anterior.
6. Depois de publica projeto hello, no menu de contexto da máquina de virtual Olá no Gerenciador de servidores, selecione **Anexar depurador...**

    O Azure obtém uma lista de processos de saudação na máquina virtual de saudação e mostra-los na caixa de diálogo de tooProcess Olá anexar.

    ![Comando Anexar depurador](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
7. Em Olá **Attach tooProcess** caixa de diálogo, selecione **selecione** tooshow somente tipos de saudação de lista de resultados de saudação toolimit de código que você deseja toodebug. Você pode depurar um código gerenciado de 32 ou 64 bits, código nativo ou ambos.

    ![Caixa de diálogo Selecionar tipo de código](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
8. Selecione processos Olá você deseja toodebug na máquina virtual de saudação e, em seguida, selecione **Attach**. Por exemplo, você pode escolher processo w3wp.exe de saudação se você desejava toodebug um aplicativo web na máquina virtual de saudação. Consulte [Depurar um o mais processos no Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) para obter mais informações.

## <a name="next-steps"></a>Próximas etapas
* Use **Intellitrace** toocollect um log de eventos de um servidor de versão e de chamadas. Consulte [Depurando um serviço de nuvem publicado com o IntelliTrace e o Visual Studio](http://go.microsoft.com/fwlink/?LinkID=623016).
* Use **diagnóstico do Azure** toolog obter informações de execução de código em funções, quer funções hello estejam em execução no ambiente de desenvolvimento de saudação ou no Azure. Consulte [Coletando dados de log usando o Diagnóstico do Azure](http://go.microsoft.com/fwlink/p/?LinkId=400450).
