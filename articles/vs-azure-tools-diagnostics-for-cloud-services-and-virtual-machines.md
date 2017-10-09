---
title: "aaaConfiguring diagnóstico para os serviços de nuvem do Azure e máquinas virtuais | Microsoft Docs"
description: "Descreve como tooconfigure informações de diagnóstico para depurar os serviços de nuvem do Azure e máquinas virtuais (VMs) no Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: e70cd7b4-6298-43aa-adea-6fd618414c26
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 74cdf49413d6d89a84195070dd9d817da2463373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-diagnostics-for-azure-cloud-services-and-virtual-machines"></a>Configurando o diagnóstico para os serviços de nuvem do Azure e máquinas virtuais
Quando você precisar tootroubleshoot um serviço de nuvem do Azure ou a máquina virtual do Azure, você pode configurar o diagnóstico do Azure mais facilmente usando o Visual Studio. Diagnóstico do Azure captura dados de sistema e dados de log em instâncias de máquina virtual que executam o serviço de nuvem e máquinas virtuais de saudação e transfere dados em uma conta de armazenamento de sua escolha. Consulte [Habilitar o registro em log de diagnóstico para aplicativos Web no Serviço de Aplicativo do Azure](app-service-web/web-sites-enable-diagnostic-log.md) para obter mais informações sobre o registro em log de diagnóstico no Azure.

Este tópico mostra como tooenable e configurar o diagnóstico do Azure no Visual Studio, antes e após a implantação, bem como em máquinas virtuais do Azure. Ele também mostra como tipos de saudação do tooselect de toocollect de informações de diagnóstico e como tooview Olá as informações depois dele.

Você pode configurar o diagnóstico do Azure no hello maneiras a seguir:

* Você pode alterar as configurações de diagnóstico por meio de saudação **configuração de diagnóstico** caixa de diálogo no Visual Studio. Olá configurações são salvas em um arquivo chamado wadcfgx (wadcfg no SDK do Azure 2.4 ou anterior). Como alternativa, você pode modificar diretamente o arquivo de configuração de saudação. Se você atualizar manualmente o arquivo hello, alterações de configuração de saudação levará Olá efeito próxima vez que você implantar Olá tooAzure de serviço de nuvem ou serviço Olá execução no emulador de saudação.
* Use **Cloud Explorer** ou **Server Explorer** nas configurações de diagnóstico do Visual Studio toochange Olá para um serviço de nuvem em execução ou a máquina virtual.

## <a name="azure-26-diagnostics-changes"></a>Alterações de diagnóstico do Azure 2.6
Para projetos de SDK 2.6 do Azure no Visual Studio, Olá as seguintes alterações foram feita. (Essas alterações também se aplicam a versões toolater do SDK do Azure.)

* emulador local Olá agora dá suporte a diagnóstico. Isso significa que você pode coletar dados de diagnóstico e certifique-se de que seu aplicativo está criando Olá rastreamentos direito enquanto você estiver desenvolvendo e testando no Visual Studio. Olá a cadeia de caracteres de conexão `UseDevelopmentStorage=true` habilita a coleta de dados de diagnóstico durante a execução do seu projeto de serviço de nuvem no Visual Studio usando o emulador de armazenamento do Azure hello. Todos os dados de diagnóstico são coletados na conta de armazenamento da saudação (armazenamento de desenvolvimento).
* cadeia de conexão de conta para armazenamento de diagnóstico Hello (windowsazure) é armazenada novamente no arquivo de configuração (. cscfg) do serviço de saudação. No Azure SDK 2.5 conta de armazenamento de diagnóstico Olá foi especificada no arquivo de wadcfgx de saudação.

Há algumas diferenças importantes entre como cadeia de caracteres de conexão Olá funcionou no SDK do Azure 2.4 e anterior e como ele funciona no Azure SDK 2.6 e posterior.

* No Azure SDK 2.4 e anterior, cadeia de caracteres de conexão Olá foi usada como um tempo de execução por Olá diagnóstico plug-in tooget Olá informações conta de armazenamento para a transferência de logs de diagnóstico.
* No Azure SDK 2.6 e posterior, a cadeia de caracteres de conexão de diagnóstico Olá é usada pela extensão de diagnóstico do Visual Studio tooconfigure Olá com informações de conta de armazenamento apropriado Olá durante a publicação. cadeia de caracteres de conexão Olá permite definir contas de armazenamento diferentes para as configurações de serviço diferente que o Visual Studio usará ao publicar. No entanto, porque o diagnóstico de saudação plug-in não está mais disponível (após 2.5 do SDK do Azure), arquivo. cscfg Olá por si só não é possível habilitar Olá extensão de diagnóstico. Você tem extensão de saudação tooenable separadamente através de ferramentas como o Visual Studio ou PowerShell.
* processo de saudação toosimplify de configuração de extensão de diagnóstico Olá com o PowerShell, saída de pacote de saudação do Visual Studio também contém Olá pública XML de configuração para extensão de diagnóstico Olá para cada função. O Visual Studio usa Olá diagnóstico conexão cadeia de caracteres toopopulate Olá armazenamento conta informações presentes na configuração pública hello. arquivos de configuração pública Olá são criados na pasta de extensões hello e seguem o padrão de saudação PaaSDiagnostics. &lt;RoleName >. PubConfig.xml. Todas as implantações do PowerShell com base podem usar este padrão toomap tooa cada configuração função.
* cadeia de caracteres de conexão de saudação no arquivo. cscfg de saudação também é usada por Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) tooaccess Olá dados de diagnóstico para que possa aparecer em hello **monitoramento** é necessária cadeia de conexão de saudação do guia. tooconfigure Olá serviço tooshow detalhado de dados no portal de saudação de monitoramento.

## <a name="migrating-projects-tooazure-sdk-26-and-later"></a>Migrando projetos tooAzure SDK 2.6 e posterior
Ao migrar do Azure SDK 2.5 tooAzure SDK 2.6 ou posterior, se você tiver uma conta de armazenamento de diagnóstico especificada no arquivo de .wadcfgx Olá, em seguida, ele permanecerá lá. contas tootake aproveitar a flexibilidade de saudação do uso de armazenamento diferentes para configurações de armazenamento diferente, você terá que toomanually Adicionar projeto de tooyour de cadeia de caracteres de conexão de saudação. Se você estiver migrando um projeto do SDK do Azure 2.4 ou tooAzure anterior 2.6 do SDK, em seguida, Olá diagnóstico cadeias de caracteres de conexão são preservadas. No entanto, observe alterações hello como cadeias de caracteres de conexão são tratadas no SDK 2.6 do Azure conforme especificado na seção anterior hello.

### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Como o Visual Studio determina a conta de armazenamento de diagnóstico Olá
* Se uma cadeia de caracteres de conexão de diagnóstico é especificada no arquivo. cscfg de hello, Visual Studio usa-extensão de diagnóstico Olá tooconfigure durante a publicação e ao gerar os arquivos de xml de configuração pública Olá durante o empacotamento.
* Se nenhuma cadeia de caracteres de conexão de diagnóstico é especificada no arquivo. cscfg de hello, em seguida, Visual Studio reverterá toousing conta de armazenamento de saudação especificada no hello .wadcfgx tooconfigure Olá diagnóstico extensão de arquivo ao publicar e gerando Olá público arquivos de xml de configuração ao empacotar.
* cadeia de conexão de diagnóstico Olá no arquivo. cscfg de saudação tem precedência sobre a conta de armazenamento Olá no arquivo de .wadcfgx hello. Se uma cadeia de caracteres de conexão de diagnóstico é especificado no arquivo. cscfg hello, em seguida, Visual Studio usa e ignora a conta de armazenamento Olá .wadcfgx.

### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>O que does hello "Atualizar cadeias de conexão de armazenamento de desenvolvimento..." faz a caixa de seleção?
Olá a caixa de seleção **atualizar cadeias de conexão de armazenamento de desenvolvimento para diagnóstico e Caching com credenciais de conta de armazenamento do Microsoft Azure ao publicar tooMicrosoft Azure** oferece uma maneira conveniente tooupdate qualquer cadeias de conexão de conta de armazenamento de desenvolvimento com a conta de armazenamento do Azure Olá especificada durante a publicação.

Por exemplo, suponha que você selecionar essa caixa de seleção e especifica a cadeia de caracteres de conexão de diagnóstico Olá `UseDevelopmentStorage=true`. Quando você publica Olá projeto tooAzure, Visual Studio atualizará automaticamente o cadeia de caracteres de conexão de diagnóstico Olá com conta de armazenamento Olá especificada no Assistente de publicação de saudação. No entanto, se uma conta de armazenamento real foi especificada como cadeia de caracteres de conexão de diagnóstico Olá, em seguida, essa conta é usada em vez disso.

## <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Diferenças de funcionalidade de diagnóstico entre SDK do Azure 2.4 e anteriores e SDK do Azure 2.5 e posteriores
Se você estiver atualizando seu projeto do Azure SDK 2.4 tooAzure SDK 2.5 ou posterior, você deve ter em Olá mente diferenças de recursos de diagnóstico a seguir.

* **APIs de configuração estão preteridos** – A configuração programática de diagnóstico está disponível no SDK do Azure 2.4 ou anteriores, mas foi preterida no SDK do Azure 2.5 e posteriores. Se sua configuração de diagnóstico está definida atualmente no código, você precisará tooreconfigure essas configurações a partir do zero no projeto migrado de saudação na ordem de trabalho de tookeep de diagnóstico. arquivo de configuração de diagnóstico Olá para o SDK do Azure 2.4 é wadcfg e wadcfgx 2.5 do SDK do Azure e posterior.
* **Diagnóstico para aplicativos de serviço de nuvem pode ser configurado somente no nível de função hello, não no nível de instância de saudação.**
* **Sempre que você implantar seu aplicativo, a configuração de diagnóstico de saudação é atualizada** – isso pode causar problemas de paridade, se você alterar a configuração de diagnóstico do Gerenciador de servidores e, em seguida, reimplante o aplicativo.
* **No Azure SDK 2.5 e posterior, despejos de memória são configurados no arquivo de configuração de diagnóstico hello, não no código** – se você tiver despejos de memória configurados no código, você terá toomanually configuração de saudação de transferência de arquivo de configuração do código toohello, porque Olá despejos de memória não são transferidos durante a saudação migração tooAzure 2.6 do SDK.

## <a name="enable-diagnostics-in-cloud-service-projects-before-deploying-them"></a>Habilitar o diagnóstico em projetos de serviço de nuvem antes de implantá-los
No Visual Studio, você pode escolher dados de diagnóstico toocollect para funções executadas no Azure, quando você executa o serviço Olá no emulador de saudação antes de implantá-lo. Todas as configurações de toodiagnostics alterações no Visual Studio são salvos no arquivo de configuração do hello wadcfgx. Essas definições de configuração especificam conta de armazenamento Olá onde os dados de diagnóstico são salvos quando você implantar o serviço de nuvem.

[!INCLUDE [cloud-services-wad-warning](../includes/cloud-services-wad-warning.md)]

### <a name="tooenable-diagnostics-in-visual-studio-before-deployment"></a>Diagnóstico de tooenable no Visual Studio antes da implantação
1. No menu de atalho Olá para função hello seu interesse, escolha **propriedades**e, em seguida, escolha Olá **configuração** guia na função de saudação **propriedades** janela.
2. Em Olá **diagnóstico** seção, certifique-se de que Olá **habilitar o diagnóstico** caixa de seleção é marcada.
   
    ![Acessando a opção de habilitar o diagnóstico Olá](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796660.png)
3. Escolha Olá reticências (...) botão toospecify Olá conta de armazenamento onde deseja Olá toobe de dados de diagnóstico armazenado. conta de armazenamento Olá que você escolher será local Olá onde os dados são armazenados.
   
    ![Especifique a saudação toouse de conta de armazenamento](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796661.png)
4. Em Olá **criar cadeia de Conexão de armazenamento** caixa de diálogo, especifique se deseja tooconnect usando Olá emulador de armazenamento do Azure, uma assinatura do Azure, ou credenciais inseridas manualmente.
   
    ![Caixa de diálogo Conta de armazenamento](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796662.png)
   
   * Se você escolher a opção de emulador de armazenamento do Microsoft Azure hello, a cadeia de conexão hello está definida tooUseDevelopmentStorage = true.
   * Se você escolher Olá sua opção de inscrição, você pode escolher Olá assinatura do Azure que você deseja que o nome da conta de toouse e hello. Você pode escolher como gerenciar contas de saudação botão toomanage suas assinaturas do Azure.
   * Se você escolher a opção de credenciais Olá inserida manualmente, você está nome de saudação tooenter solicitada e a chave de saudação conta do Azure que você deseja toouse.
5. Escolha Olá **configurar** saudação do botão tooview **configuração de diagnóstico** caixa de diálogo. Cada guia (exceto **Geral** e **Diretórios de log**) representa uma fonte de dados de diagnóstico que você pode coletar. Guia de padrão de saudação, **geral**, oferece Olá seguintes opções de coleta de dados de diagnóstico: **somente erros**, **todas as informações de**, e **plano personalizado** . Olá opção padrão, **somente erros**, leva Olá menor quantidade de armazenamento porque ele não é transferida avisos ou mensagens de rastreamento. Olá, todas as transferências de opção de informações Olá a maioria das informações e é, portanto, Olá a opção mais cara em termos de armazenamento.
   
    ![Habilitar a configuração e diagnóstico do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
6. Neste exemplo, selecione Olá **plano personalizado** opção para que você pode personalizar Olá dados coletados.
7. Olá **cota de disco em MB** Especifica quanto espaço que deseja tooallocate na conta de seu armazenamento para dados de diagnóstico. Você pode alterar o valor padrão de saudação se desejar.
8. Em cada guia de dados de diagnóstico que você deseja toocollect, selecione seu **Habilitar transferência de <log type>**  caixa de seleção. Por exemplo, se você quiser toocollect logs de aplicativos, selecione Olá **Habilitar transferência de Logs do aplicativo** caixa de seleção Olá **Logs de aplicativo** guia. Além disso, especifique outras informações necessárias para cada tipo de dados de diagnóstico. Consulte a seção Olá **configurar fontes de dados de diagnóstico** mais adiante neste tópico para obter informações de configuração em cada guia.
9. Depois de habilitar a coleção de todos os dados de diagnóstico de saudação desejado, escolha Olá **Okey** botão.
10. Execute seu projeto de serviço de nuvem do Azure no Visual Studio, como de costume. Como você usa seu aplicativo, informações de log Olá que você habilitou é salvo toohello conta de armazenamento do Azure especificada.

## <a name="enable-diagnostics-in-azure-virtual-machines"></a>Habilitar o diagnóstico em máquinas virtuais do Azure
No Visual Studio, você pode escolher os dados de diagnóstico toocollect para máquinas virtuais do Azure.

### <a name="tooenable-diagnostics-in-azure-virtual-machines"></a>Diagnóstico de tooenable em máquinas virtuais do Azure
1. Em **Server Explorer**, escolha Olá nó do Azure e, em seguida, conecte-se tooyour assinatura do Azure, se você ainda não estiver conectado.
2. Expanda Olá **máquinas virtuais** nó. Você pode criar uma nova máquina virtual ou selecione uma que já está lá.
3. No menu de atalho Olá para a máquina virtual Olá seu interesse, escolha **configurar**. Isso mostra a caixa de diálogo de configuração de máquina virtual de saudação.
   
    ![Configurando uma máquina virtual do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796663.png)
4. Se ele ainda não estiver instalado, adicione a extensão de diagnóstico de agente de monitoramento Microsoft hello. Essa extensão permite coletar dados de diagnóstico para Olá máquina virtual do Azure. Na lista de extensões instalado hello, escolha Olá selecione uma extensão disponível lista suspensa menu e clique em Diagnóstico de agente de monitoramento Microsoft.
   
    ![Instalando uma extensão de máquina virtual do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766024.png)
   
   > [!NOTE]
   > Outras extensões de diagnóstico estão disponíveis para as máquinas virtuais. Para obter mais informações, consulte recursos e extensões de VM do Azure.
   > 
   > 
5. Escolha Olá **adicionar** botão extensão de saudação tooadd e exibir seu **configuração de diagnóstico** caixa de diálogo.
6. Escolha Olá **configurar** botão toospecify uma conta de armazenamento e, em seguida, escolha Olá **Okey** botão.
   
    Cada guia (exceto **Geral** e **Diretórios de log**) representa uma fonte de dados de diagnóstico que você pode coletar.
   
    ![Habilitar a configuração e diagnóstico do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
   
    Guia de padrão de saudação, **geral**, oferece Olá seguintes opções de coleta de dados de diagnóstico: **somente erros**, **todas as informações de**, e **plano personalizado** . Olá opção padrão, **somente erros**, leva Olá menor quantidade de armazenamento porque ele não é transferida avisos ou mensagens de rastreamento. Olá **todas as informações** transferências de opção Olá a maioria das informações e é, portanto, a opção mais cara Olá em termos de armazenamento.
7. Neste exemplo, selecione Olá **plano personalizado** opção para que você pode personalizar Olá dados coletados.
8. Olá **cota de disco em MB** Especifica quanto espaço que deseja tooallocate na conta de seu armazenamento para dados de diagnóstico. Você pode alterar o valor padrão de saudação se desejar.
9. Em cada guia de dados de diagnóstico que você deseja toocollect, selecione seu **Habilitar transferência de <log type>**  caixa de seleção.
   
    Por exemplo, se você quiser toocollect logs de aplicativos, selecione Olá **Habilitar transferência de Logs do aplicativo** caixa de seleção Olá **Logs de aplicativo** guia. Além disso, especifique outras informações necessárias para cada tipo de dados de diagnóstico. Consulte a seção Olá **configurar fontes de dados de diagnóstico** mais adiante neste tópico para obter informações de configuração em cada guia.
10. Depois de habilitar a coleção de todos os dados de diagnóstico de saudação desejado, escolha Olá **Okey** botão.
11. Salve o projeto de saudação atualizado.
    
     Você verá uma mensagem de saudação **Log de atividades do Microsoft Azure** janela Olá máquina virtual foi atualizada.

## <a name="configure-diagnostics-data-sources"></a>Configurar fontes de dados de diagnóstico
Depois de habilitar a coleta de dados de diagnóstico, você pode escolher quais fontes de dados exatamente como você deseja toocollect e quais informações são coletadas. Olá, esta é uma lista de guias no hello **configuração de diagnóstico** caixa de diálogo e significa que cada opção de configuração.

### <a name="application-logs"></a>Logs de aplicativo
**Logs de aplicativos** contêm informações de diagnóstico produzidas por um aplicativo Web. Se você quiser toocapture logs de aplicativos, selecione Olá **Habilitar transferência de Logs do aplicativo** caixa de seleção. Você pode aumentar ou diminuir Olá número de minutos quando os logs de aplicativo hello são transferidas tooyour conta de armazenamento por meio da alteração Olá **o período de transferência (min)** valor. Você também pode alterar a quantidade de saudação de informações capturadas no log de saudação definindo o valor do nível de Log hello. Por exemplo, você pode escolher **detalhado** tooget obter mais informações ou escolha **crítico** erros críticos apenas toocapture. Se você tiver um provedor de diagnósticos específicos que emite os logs de aplicativo, você pode capturá-los adicionando toohello GUID do provedor Olá **provedor GUID** caixa.

  ![Logs de aplicativo](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758145.png)

  Consulte [Habilitar o registro em log de diagnóstico para aplicativos Web no Serviço de Aplicativo do Azure](app-service-web/web-sites-enable-diagnostic-log.md) para obter mais informações sobre os logs de aplicativo.

### <a name="windows-event-logs"></a>Logs de eventos do Windows
Se você quiser toocapture logs de eventos do Windows, selecione Olá **Habilitar transferência de Logs de eventos do Windows** caixa de seleção. Você pode aumentar ou diminuir Olá número de minutos quando os logs de eventos de saudação são transferidas tooyour conta de armazenamento por meio da alteração Olá **o período de transferência (min)** valor. Marque as caixas de seleção de saudação para tipos de saudação de eventos que você deseja tootrack.

  ![Logs de eventos](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796664.png)

Se você estiver usando o SDK do Azure 2.6 ou posterior e deseja toospecify uma fonte de dados personalizado, insira-o no hello  **<Data source name>**  texto caixa e, em seguida, escolha Olá **adicionar** tooit próximo botão. fonte de dados de saudação é adicionado toohello diagnostics.cfcfg arquivo.

Se você estiver usando o Azure SDK 2.5 e deseja toospecify uma fonte de dados personalizada, você pode adicioná-lo toohello `WindowsEventLog` seção Olá wadcfgx de arquivo, como Olá exemplo a seguir.

```
<WindowsEventLog scheduledTransferPeriod="PT1M">
   <DataSource name="Application!*" />
   <DataSource name="CustomDataSource!*" />
</WindowsEventLog>
```
### <a name="performance-counters"></a>Contadores de desempenho
As informações do contador de desempenho podem ajudá-lo a localizar afunilamentos do sistema e ajustar o sistema e desempenho do aplicativo. Consulte [Criar e usar contadores de desempenho em um aplicativo do Azure](https://msdn.microsoft.com/library/azure/hh411542.aspx) para obter mais informações. Se você quiser toocapture contadores de desempenho, selecione Olá **Habilitar transferência de contadores de desempenho** caixa de seleção. Você pode aumentar ou diminuir Olá número de minutos quando os logs de eventos de saudação são transferidas tooyour conta de armazenamento por meio da alteração Olá **o período de transferência (min)** valor. Selecione as caixas de seleção de saudação para hello contadores de desempenho que você deseja tootrack.

  ![Contadores de desempenho](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758147.png)

tootrack um contador de desempenho não estiver listado, insira-o usando Olá sintaxe sugerida e escolha Olá **adicionar** botão. sistema operacional de saudação na máquina virtual de saudação determina quais contadores de desempenho que você pode controlar. Para obter mais informações sobre a sintaxe, consulte [Especificando um caminho de contador](https://msdn.microsoft.com/library/windows/desktop/aa373193.aspx).

### <a name="infrastructure-logs"></a>Logs de infraestrutura
Se você quiser que os logs de infraestrutura de toocapture, que contêm informações sobre Olá infraestrutura de diagnóstica do Azure, o módulo RemoteAccess de saudação e o módulo RemoteForwarder de saudação, selecione Olá **Habilitar transferência de Logs de infraestrutura**caixa de seleção. Você pode aumentar ou diminuir Olá número de minutos quando Olá logs são transferidas tooyour conta de armazenamento, alterando o valor do período de transferência (min) de saudação.

  ![Logs de infraestrutura de diagnósticos](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758148.png)

  Para saber mais, consulte [Coletar dados do log usando o Diagnóstico do Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx) .

### <a name="log-directories"></a>Diretórios de log
Se você quiser que os diretórios de log de toocapture, que contêm os dados coletados de diretórios de log de solicitações de serviços de informações da Internet (IIS), solicitações com falha ou pastas que você escolher, selecione Olá **Habilitar transferência de diretórios de Log**caixa de seleção. Você pode aumentar ou diminuir Olá número de minutos quando Olá logs são transferidas tooyour conta de armazenamento por meio da alteração Olá **o período de transferência (min)** valor.

Você pode marcar as caixas de saudação de logs Olá deseja toocollect, como **Logs do IIS** e **solicitação com falha** Logs. Nomes de contêiner de armazenamento padrão são fornecidos, mas você pode alterar os nomes de saudação se você quiser.

Além disso, você pode capturar logs de qualquer pasta. Especifique apenas o caminho de saudação no Olá **Log do diretório absoluto** seção e, em seguida, escolha Olá **Adicionar diretório** botão. Olá logs serão capturados toohello especificado contêineres.

  ![Diretórios de log](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796665.png)

### <a name="etw-logs"></a>Logs do ETW
Se você usar [de rastreamento de eventos do Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) (ETW) e desejar que os logs do ETW toocapture, selecione Olá **Habilitar transferência de Logs do ETW** caixa de seleção. Você pode aumentar ou diminuir Olá número de minutos quando Olá logs são transferidas tooyour conta de armazenamento por meio da alteração Olá **o período de transferência (min)** valor.

Olá eventos são capturados de fontes de evento e manifestos de eventos que você especificar. toospecify uma fonte de evento, insira um nome no hello **fontes de evento** seção e, em seguida, escolha Olá **Adicionar origem do evento** botão. Da mesma forma, você pode especificar um manifesto de evento em Olá **manifestos de eventos** seção e, em seguida, escolha Olá **adicionar manifesto de evento** botão.

  ![Logs do ETW](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766025.png)

  há suporte para no ASP.NET framework do ETW Olá por meio de classes em Olá [System.Diagnostics.aspx] (namespace https://msdn.microsoft.com/library/system.diagnostics (v=vs.110). Olá Microsoft.WindowsAzure.Diagnostics namespace, que herda e estende o padrão [System.Diagnostics.aspx] (classes de https://msdn.microsoft.com/library/system.diagnostics (v=vs.110), habilita Olá uso de [System.Diagnostics.aspx] ( https://msdn.microsoft.com/library/System.Diagnostics (v=vs.110) como uma estrutura de registro em log no hello ambiente do Azure. Para obter mais informações, consulte [Tomar controle de registro em log e rastreamento no Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) e [Habilitando o diagnóstico no serviços de nuvem e Máquinas virtuais do Azure](cloud-services/cloud-services-dotnet-diagnostics.md).

### <a name="crash-dumps"></a>Despejos de falhas
Se você quiser toocapture informações sobre quando uma instância de função falha, selecione Olá **Habilitar transferência de despejos** caixa de seleção. (Pelo fato do ASP.NET manipular mais exceções, isso geralmente é útil somente para uma função de trabalho.) Você pode aumentar ou diminuir a porcentagem de saudação do armazenamento espaço dedicado toohello despejos alterando Olá **cota de diretório (%)** valor. Você pode alterar o contêiner de armazenamento Olá onde Olá despejos de memória são armazenados, e você pode selecionar se deseja toocapture um **completo** ou **Mini** despejo.

processos Hello está sendo controlados no momento estão listados. Marque as caixas de seleção de saudação para processos de saudação que você deseja toocapture. tooadd outra lista de toohello de processo, digite o nome do processo de saudação e escolha Olá **adicionar processo** botão.

  ![Despejos de falhas](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766026.png)

  Consulte [Tomar controle do registro em log e rastreamento no Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) e [Diagnóstico do Microsoft Azure parte 4: componentes de registro de log personalizados e alterações do Diagnóstico do Azure 1.3](http://justazure.com/microsoft-azure-diagnostics-part-4-custom-logging-components-azure-diagnostics-1-3-changes/) para obter mais informações.

## <a name="view-hello-diagnostics-data"></a>Saudação de exibir dados de diagnóstico
Depois que você coletou dados de diagnóstico de saudação para um serviço de nuvem ou uma máquina virtual, você pode exibi-lo.

### <a name="tooview-cloud-service-diagnostics-data"></a>dados de diagnóstico de serviço de nuvem tooview
1. Implante seu serviço de nuvem como de costume e, em seguida, execute-o.
2. Você pode exibir dados de diagnóstico de saudação em um relatório que o Visual Studio gera ou tabelas em sua conta de armazenamento. dados de saudação tooview em um relatório, abra **Cloud Explorer** ou **Server Explorer**, abra o menu de atalho de saudação do nó Olá para função hello seu interesse e, em seguida, escolha **exibir dados de diagnóstico** .
   
    ![Exibir dados de diagnóstico](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748912.png)
   
    Um relatório que mostra dados de saudação disponíveis é exibida.
   
    ![Relatório do Microsoft Azure Diagnostics no Visual Studio](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796666.png)
   
    Se os dados mais recentes Olá não aparecem, você pode ter toowait para tooelapse de período de transferência hello.
   
    Escolha Olá **atualizar** vincular tooimmediately atualização Olá dados ou escolher um intervalo em Olá **atualização automática** dados suspensa lista caixa toohave saudação atualizados automaticamente. dados de erro de saudação tooexport, escolha Olá **exportar tooCSV** botão toocreate um arquivo de valores separados por vírgulas, você pode abrir em uma planilha.
   
    No **Cloud Explorer** ou **Server Explorer**, abra a conta de armazenamento Olá associado à implantação de saudação.
3. Abrir tabelas de diagnóstico de saudação no Visualizador de tabela hello e examine Olá dados coletados. Para logs do IIS e os logs personalizados, você pode abrir um contêiner de blob. Revisando Olá a tabela a seguir, você pode encontrar hello tabela ou contêiner de blob que contém dados de saudação que lhe interessam. Além disso toohello dados para que o arquivo de log, as entradas da tabela Olá contenham EventTickCount, DeploymentId, função e RoleInstance toohelp identificar qual máquina virtual e a função gerado dados saudação e quando. 
   
   | Dados de diagnóstico | Descrição | Local |
   | --- | --- | --- |
   | Logs de aplicativo |Logs gerados pelo seu código chamando métodos da classe Trace da saudação. |WADLogsTable |
   | Logs de eventos |Esses dados são dos logs de eventos do Windows hello em máquinas virtuais de saudação. O Windows armazena informações nesses logs, mas aplicativos e serviços também usá-los tooreport erros ou informações de log. |WADWindowsEventLogsTable |
   | Contadores de desempenho |Você pode coletar dados em qualquer contador de desempenho está disponível na máquina virtual de saudação. sistema operacional de saudação fornece contadores de desempenho, que incluem estatísticas, como tempo de processador e uso de memória. |WADPerformanceCountersTable |
   | Logs de infraestrutura |Esses logs são gerados de infraestrutura de diagnóstico de saudação em si. |WADDiagnosticInfrastructureLogsTable |
   | Logs IIS |Esses logs registram solicitações da Web. Se seu serviço de nuvem obtém uma quantidade significativa de tráfego, esses logs podem ser muito longos. Portanto, você deve coletar e armazenar esses dados somente quando forem necessários. |Você pode encontrar os logs de solicitação com falha no contêiner de blob Olá em wad-iis-failedreqlogs em um caminho para essa implantação, a função e a instância. Você pode encontrar logs completos em wad-iis-logfiles. As entradas para cada arquivo são feitas na tabela de WADDirectories hello. |
   | Despejos de falhas |Essas informações fornecem imagens binárias do processo do serviço de nuvem (normalmente uma função de trabalho). |contêiner de blob wad-crush-dumps |
   | Arquivos de log personalizados |Logs de dados que você predefiniu. |Você pode especificar no local de saudação do código personalizado de arquivos de log em sua conta de armazenamento. Por exemplo, você pode especificar um contêiner de blob personalizado. |
4. Se qualquer tipo de dados são truncados, você pode tentar crescentes buffer Olá para esse tipo de dados ou encurtar o intervalo de saudação entre transferências de dados da conta de armazenamento de tooyour Olá máquina virtual.
5. (opcional) Limpeza de dados do armazenamento de saudação conta ocasionalmente tooreduce custos gerais de armazenamento.
6. Quando você fizer uma implantação completa, arquivo de diagnostics.cscfg hello (.wadcfgx 2.5 do SDK do Azure) é atualizado no Azure e seu serviço de nuvem pega qualquer configuração de diagnóstico de tooyour de alterações. Se, em vez disso, atualizar uma implantação existente, o arquivo. cscfg de saudação não será atualizado no Azure. Você ainda pode alterar as configurações de diagnóstico, no entanto, seguindo as etapas Olá Olá próxima seção. Para obter mais informações sobre como executar uma implantação completa e atualizar uma implantação existente, consulte [Assistente de publicação de aplicativo no Azure](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="tooview-virtual-machine-diagnostics-data"></a>dados de diagnóstico de máquina virtual tooview
1. No menu de atalho Olá para a máquina virtual de saudação, escolha **exibir dados de diagnóstico**.
   
    ![Exibir dados de diagnóstico na máquina virtual do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766027.png)
   
    Isso abre o hello **resumo de diagnóstico** janela.
   
    ![Resumo de diagnóstico de máquina virtual do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796667.png)  
   
    Se os dados mais recentes Olá não aparecem, você pode ter toowait para tooelapse de período de transferência hello.
   
    Escolha Olá **atualizar** vincular tooimmediately atualização Olá dados ou escolher um intervalo em Olá **atualização automática** dados suspensa lista caixa toohave saudação atualizados automaticamente. dados de erro de saudação tooexport, escolha Olá **exportar tooCSV** botão toocreate um arquivo de valores separados por vírgulas, você pode abrir em uma planilha.

## <a name="configure-cloud-service-diagnostics-after-deployment"></a>Configurar o diagnóstico de serviço de nuvem após a implantação
Se você estiver investigando um problema com um serviço de nuvem que já em execução, convém toocollect dados que você não especificou antes de você função hello originalmente implantado. Nesse caso, você pode iniciar toocollect dados usando configurações de saudação do Gerenciador de servidores. Você pode configurar o diagnóstico para uma única instância ou todas as instâncias de saudação em uma função, dependendo se você abre a caixa de diálogo de configuração de diagnóstico de Olá no menu de atalho Olá para instância de saudação ou função hello. Se você configurar o nó da função hello, as alterações se aplicam a tooall instâncias. Se você configurar o nó da instância Olá, as alterações se aplicam apenas a instância toothat.

### <a name="tooconfigure-diagnostics-for-a-running-cloud-service"></a>Diagnóstico de tooconfigure para um serviço de nuvem em execução
1. No Gerenciador de servidores, expanda Olá **serviços de nuvem** nó e em seguida, expanda a função de saudação toolocate nós ou a instância que você deseja tooinvestigate ou ambos.
   
    ![Configurando o diagnóstico](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748913.png)
2. No menu de atalho Olá para um nó da instância ou um nó de função, escolha **as configurações de diagnóstico de atualização**e escolha as configurações de diagnóstico que você deseja toocollect hello.
   
    Para obter informações sobre definições de configuração hello, consulte **configurar fontes de dados de diagnóstico** neste tópico. Para obter informações sobre como tooview Olá dados de diagnóstico, consulte **exibir dados de diagnóstico de saudação** neste tópico.
   
    Se você alterar a coleta de dados no **Gerenciador de Servidores**, essas alterações permanecerão em vigor até que você reimplante totalmente o seu serviço de nuvem. Se você usar configurações de publicação padrão hello, Olá alterações não são substituídas, desde que o padrão de saudação publicar a configuração é implantação existente do tooupdate hello, em vez de fazer uma reimplantação completa. Limpar as configurações de saudação se toomake no momento da implantação, vá toohello **configurações avançadas** guia no Assistente de publicação hello e limpar Olá **atualização de implantação** caixa de seleção. Ao reimplantar com essa caixa de seleção desmarcada, as configurações de saudação reverter toothose no arquivo de saudação .wadcfgx (ou wadcfg) conforme definido por meio do editor de propriedades de saudação para função hello. Se você atualizar sua implantação, o Azure mantém as configurações antigas do hello.

## <a name="troubleshoot-azure-cloud-service-issues"></a>Solucionar problemas do serviço de nuvem do Azure
Se você tiver problemas com seus projetos de serviço de nuvem, como uma função que travou em um status "ocupado", repetidamente recicla ou gera um erro interno do servidor, há ferramentas e técnicas que você pode usar toodiagnose e corrigir esses problemas. Para exemplos específicos de problemas comuns e soluções, bem como uma visão geral dos conceitos de saudação e ferramentas usados toodiagnose e corrigir esses erros, consulte [dados de diagnóstico de computação do Azure PaaS](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

## <a name="q--a"></a>Perguntas e respostas
**O que é o tamanho do buffer de saudação e o tamanho deve ser?**

Em cada instância de máquina virtual, as cotas limitam quantos dados de diagnósticos que podem ser armazenados no sistema de arquivos local hello. Além disso, você pode especificar um tamanho do buffer para cada tipo de dados de diagnóstico disponíveis. Esse tamanho do buffer age como uma cota individual para esse tipo de dados. Verificando inferior Olá Olá da caixa de diálogo, você pode determinar Olá cota geral e a quantidade de saudação de memória que permanece. Se você especificar buffers maiores ou mais tipos de dados, você deverá abordar Olá cota geral. Você pode alterar Olá cota geral modificando o arquivo de configuração diagnostics.wadcfg/.wadcfgx hello. Olá diagnóstico dados são armazenados em Olá mesmo sistema de arquivos como dados do aplicativo, para que se seu aplicativo usa muito espaço em disco, você não deve aumentar Olá cota geral do diagnóstico.

**O que é o período de transferência hello e quanto tempo deve ser?**

o período de transferência Olá é Olá tempo que captura a decorrer entre os dados. Depois de cada período de transferência, os dados são movidos do sistema de arquivos local Olá em tootables uma máquina virtual em sua conta de armazenamento. Se o quantidade de saudação de dados que são coletados excede a cota de saudação antes do final de saudação de um período de transferência, os dados mais antigos serão descartados. Talvez você queira toodecrease o período de transferência Olá se você estiver perda de dados porque seus dados excedem o tamanho do buffer hello ou Olá cota geral.

**Fuso horário são Olá carimbos de hora?**

os carimbos de hora Olá estão no fuso horário local de saudação do hello data center que hospeda o serviço de nuvem. Olá seguintes três colunas de carimbo de hora nas tabelas de log hello são usadas.

* **PreciseTimeStamp** é Olá ETW carimbo de hora Olá evento. Ou seja, o evento Olá Olá é registrado de cliente de saudação.
* **Carimbo de hora** é PreciseTimeStamp arredondado para baixo de limite de frequência de carregamento de toohello. Assim, se sua frequência de carregamento é 5 minutos e o evento Olá tempo 12:17:00, o carimbo de hora será 15:00:00.
* **Carimbo de hora** é Olá carimbo de hora na qual Olá entidade foi criada no hello tabela do Azure.

**Como gerenciar custos ao coletar informações de diagnóstico?**

Olá configurações padrão (**nível de Log** definido muito**erro** e **o período de transferência** definido muito**1 minuto**) são projetado toominimize custo. Os custos de computação aumentará, se você coleta mais dados de diagnóstico ou diminua o período de transferência hello. Não colete mais dados que você precisa e não se esqueça de coleta de dados toodisable quando você não precisa mais dela. Você pode sempre habilitá-lo novamente, mesmo em tempo de execução, conforme mostrado na seção anterior hello.

**Como posso coletar logs de solicitação com falha do IIS?**

Por padrão, o IIS não coleta logs de solicitação com falha. Você pode configurar o IIS toocollect-los, se você editar Olá para sua função web. config.

**Não estou obtendo informações de rastreamento de métodos RoleEntryPoint como OnStart. O que está errado?**

métodos de saudação do RoleEntryPoint são chamados no contexto de saudação do WAIISHost.exe, não o IIS. Portanto, Olá informações de configuração no Web. config que normalmente permite rastreamento não se aplica. tooresolve esse problema, adicione um projeto de função da web. config arquivo tooyour e nomeie Olá arquivo toomatch Olá assembly de saída que contém o código de RoleEntryPoint hello. No projeto de função da web saudação padrão, o nome de saudação do arquivo. config de saudação seria WAIISHost.exe.config. Em seguida, adicione Olá arquivo toothis de linhas a seguir:

```
<system.diagnostics>
  <trace>
      <listeners>
          <add name “AzureDiagnostics” type=”Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener”>
              <filter type=”” />
          </add>
      </listeners>
  </trace>
</system.diagnostics>
```

Agora, em Olá **propriedades** janela, Olá conjunto **copiar tooOutput diretório** propriedade muito**copiar sempre**.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre o diagnóstico de log no Azure, consulte [habilitando o diagnóstico nos serviços de nuvem do Azure e máquinas virtuais](cloud-services/cloud-services-dotnet-diagnostics.md) e [habilitar o log de diagnóstico para aplicativos web no serviço de aplicativo do Azure](app-service-web/web-sites-enable-diagnostic-log.md).

