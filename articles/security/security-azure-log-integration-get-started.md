---
title: "aaaGet iniciado com a integração de log do Azure | Microsoft Docs"
description: "Saiba como tooinstall hello Azure serviço de integração de log e integrar os logs de armazenamento do Azure, os Logs de auditoria do Azure e de alertas da Central de segurança do Azure."
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 53f67a7c-7e17-4c19-ac5c-a43fabff70e1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 07/26/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 26c19070d76ff73b1bdbd32ba77fb04978af387e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-with-azure-diagnostics-logging-and-windows-event-forwarding"></a>Integração do log do Azure com o log de diagnóstico do Azure e encaminhamento de eventos do Windows
Integração de Log do Azure (AzLog) permite que você toointegrate de logs bruto de recursos do Azure em seus sistemas de gerenciamento de eventos (SIEM) e informações de segurança local. Essa integração torna possível toohave um painel de segurança unificado para todos os seus ativos, local ou na nuvem hello, para que você pode agregar, correlacionar, analisar e alertas para eventos de segurança associados a seus aplicativos.
>[!NOTE]
Para obter mais informações sobre a integração de Log do Azure, você pode examinar Olá [visão geral da integração do Azure Log](https://docs.microsoft.com/azure/security/security-azure-log-integration-overview).

Este artigo o ajudará a começar com a integração de Log do Azure, concentrando-se na instalação de saudação do hello Azlog service e serviço Olá integrando o diagnóstico do Azure. Olá serviço de integração do Azure Log será capaz de toocollect informações de Log de eventos do Windows de saudação canal de eventos de segurança do Windows de máquinas virtuais implantadas no Azure IaaS. Isso é muito semelhante muito "Encaminhamento de eventos" que você pode ter usado no local.

>[!NOTE]
>saída de hello Olá capacidade toobring de integração de log do Azure no toohello SIEM é fornecido pelo Olá SIEM em si. Consulte o artigo de saudação [integração do Azure Log integração com o SIEM local](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) para obter mais informações.

toobe muito clara - Olá serviço de integração de Log do Azure é executado em um computador físico ou virtual que está usando Olá Windows Server 2008 R2 ou acima do sistema operacional (Windows Server 2012 R2 ou Windows Server 2016 são preferenciais).

computador físico Olá pode executar no local (ou em um site de hoster). Se você escolher o serviço de integração do Azure Log Olá toorun em uma máquina virtual, que a máquina virtual pode ser localizado no local ou em uma nuvem pública, como o Microsoft Azure.

Olá físico ou máquina virtual que executa o serviço de integração do Azure Log Olá requer conectividade de rede toohello nuvem pública do Azure. As etapas neste artigo fornecem detalhes sobre a configuração de saudação.

## <a name="prerequisites"></a>Pré-requisitos
No mínimo, a instalação de saudação do AzLog requer Olá itens a seguir:
* Uma **assinatura do Azure**. Se você não tiver uma, poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).
* Um **conta de armazenamento** que pode ser usado para o log de diagnóstico do Windows Azure (você pode usar uma conta de armazenamento pré-configuradas ou criar um novo – é demonstrar como tooconfigure Olá conta de armazenamento neste artigo)
  >[!NOTE]
  Dependendo do cenário, poderá não ser necessário ter uma conta de armazenamento. Olá para o cenário de diagnóstico do Azure abordadas neste artigo necessário.
* **Dois sistemas**: um computador que executará o serviço de integração do Azure Log hello e um computador que será monitorado e ter suas informações de log enviadas a máquina de serviço Azlog toohello.
   * Um computador que você deseja toomonitor – isso é uma VM em execução como um [Máquina Virtual do Azure](../virtual-machines/virtual-machines-windows-overview.md)
   * Um computador que executará o serviço de integração do Azure log Olá; Esta máquina coletará todas as informações de log hello mais tarde serão importadas para o SIEM.
    * Esse sistema pode ser local ou no Microsoft Azure.  
    * Ele precisa toobe executando x64 versão do Windows server 2008 R2 SP1 ou posterior e ter o .NET 4.5.1 instalado. Você pode determinar Olá .NET versão instalada pelo seguinte artigo Olá intitulado [como: determinar qual .NET Framework versões estão instaladas](https://msdn.microsoft.com/library/hh925568)  
    Ele deve ter conectividade toohello conta de armazenamento Azure usada para o log de diagnóstico do Azure. Forneceremos as instruções sobre como confirmar essa conectividade posteriormente neste artigo

Para ver uma demonstração rápida do processo de saudação de criar uma máquina virtual usando o portal do Azure de saudação dar uma olhada Olá vídeo abaixo.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Create-a-Virtual-Machine/player]



## <a name="deployment-considerations"></a>Considerações de implantação
Ao testar a integração do registro do Azure, você pode usar qualquer sistema que atenda aos requisitos de sistema operacional mínimo hello. No entanto, para uma saudação do ambiente de produção carga pode exigir você tooplan para escalar verticalmente ou horizontalmente.

Se o volume de eventos é alto, você pode executar várias instâncias do serviço de integração do Azure Log hello (uma instância por máquina virtual ou física). Além disso, você pode balancear a carga contas de armazenamento de diagnóstico do Azure para Windows (WAD) e o número de saudação de instâncias de toohello tooprovide assinaturas devem ser baseadas em sua capacidade.
>[!NOTE]
No momento, não temos recomendações específicas para quando tooscale as instâncias do Azure log máquinas de integração (ou seja, computadores que estão executando o serviço de integração do Azure log Olá), ou contas de armazenamento ou assinaturas. Decisões de escala devem ser baseadas na observações do desempenho em cada uma dessas áreas.

Você também tem Olá opção tooscale backup toohelp de serviço de integração do Azure Log Olá melhorar o desempenho. Olá métricas de desempenho a seguir pode ajudá-lo a dimensionamento máquinas Olá que você escolha o serviço de integração do toorun Olá logs do Azure:
* Em uma máquina com oito processadores (núcleos), uma única instância do Integrador do Azlog pode processar cerca de 24 milhões de eventos por dia (~1M/hora).

* Em um computador com quatro processadores (núcleos), uma única instância do integrador Azlog pode processar cerca de 1,5 milhão de eventos por dia (~62,5K/hora).

## <a name="install-azure-log-integration"></a>Instalar a integração do log do Azure
tooinstall integração de Log do Azure, você precisa Olá toodownload [integração do Azure log](https://www.microsoft.com/download/details.aspx?id=53324) arquivo de instalação. Percorra a rotina de instalação hello e decidir se deseja tooprovide tooMicrosoft de informações de telemetria.  

![Tela de instalação com caixa de telemetria marcada](./media/security-azure-log-integration-get-started/telemetry.png)

*
> [!NOTE]
> É recomendável permitir que os dados de telemetria do Microsoft toocollect. Você pode desativar a coleta dos dados de telemetria desmarcando essa opção.
>


Olá serviço de integração do Azure Log coleta dados de telemetria do computador de saudação no qual ele está instalado.  

Os dados de telemetria coletados são:

* Exceções que ocorrem durante a execução da integração do log do Azure
* Métricas sobre o número de saudação de consultas e eventos processados
* Estatísticas sobre quais opções de linha de comando do Azlog.exe estão sendo usadas

o processo de instalação Olá é abordado em Olá vídeo abaixo.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Install-Azure-Log-Integration/player]



## <a name="post-installation-and-validation-steps"></a>Etapas pós-instalação e validação
Depois de concluir a rotina de instalação básica do hello, estiver pronto etapa tooperform post instalação e validação de etapas:
1. Abra uma janela do PowerShell com privilégios elevados e navegue muito**c:\Program Files\Microsoft Azure Log integração**
2. Olá primeiro passo tootake é Olá tooget que azlog Cmdlets importados. Você pode fazer isso executando o script hello **LoadAzlogModule.ps1** (aviso Olá ". \" no comando a seguir de saudação). Digite **.\LoadAzlogModule.ps1** e pressione **ENTER**.  
Você verá algo parecido com o que é exibido na figura de saudação abaixo. </br></br>
![Tela de instalação com caixa de telemetria marcada](./media/security-azure-log-integration-get-started/loaded-modules.png) </br></br>
3. Agora, é necessário tooconfigure AzLog toouse um ambiente do Azure específico. Um "ambiente Azure" é hello "tipo" do Centro de dados de nuvem do Azure com que você deseja toowork. Embora haja vários ambientes do Azure no momento, opções relevantes no momento da saudação são **AzureCloud** ou **AzureUSGovernment**.   Em seu ambiente do PowerShell com privilégios elevados, verifique se você está em **c:\program files\Microsoft Azure Log Integration\** </br></br>
    Uma vez, execute o comando de saudação: </br>
    ``Set-AzlogAzureEnvironment -Name AzureCloud`` (para Azure comercial)

      >[!NOTE]
      Quando o comando Olá for bem-sucedido, você não receberá nenhum feedback.  Se você quiser toouse Olá US Government Azure cloud, você usaria **AzureUSGovernment** (para hello - variável do nome) para Olá nuvem do governo dos EUA. Não há suporte para outras nuvens do Azure no momento.  
4. Para monitorar um sistema, você precisará nome Olá Olá da conta de armazenamento em uso para diagnóstico do Azure.  No hello portal do Azure navegue muito**máquinas virtuais** e procure por máquina virtual Olá que você irá monitorar. Em Olá **propriedades** , escolha **configurações de diagnóstico**.  Clique em **agente** e anote o nome de conta de armazenamento Olá especificado. Você precisará desse nome de conta para uma etapa posterior.
![Configurações do Diagnóstico do Azure](./media/security-azure-log-integration-get-started/storage-account-large.png) </br></br>

      ![Configurações do Diagnóstico do Azure](./media/security-azure-log-integration-get-started/azure-monitoring-not-enabled-large.png)
      >[!NOTE]
      Se o monitoramento não foi habilitado durante a criação da máquina virtual será oferecida a você Olá opção tooenable como mostrado acima.
5. Agora podemos alternará toohello de voltar nossa atenção máquina de integração de log do Azure. É preciso tooverify que você tem conectividade toohello conta de armazenamento do sistema de saudação onde você instalou a integração de Log do Azure. computador físico Hello ou máquina virtual em execução Olá integração do Azure Log serviço precisa acessar as informações de tooretrieve conta armazenamento toohello registradas pelo diagnóstico do Azure conforme configurado em cada Olá monitorados sistemas.  
  1. Você pode baixar o Gerenciador de Armazenamento do Azure [aqui](http://storageexplorer.com/).
  2. Percorra a rotina de instalação Olá
  3. Depois que a conclusão da instalação de saudação clique **próximo** e deixe a caixa de seleção Olá **iniciar o Microsoft Azure Storage Explorer** marcada.  
  4. Faça logon em tooAzure.
  5. Verifique se que você pode ver a conta de armazenamento Olá que você configurou para diagnóstico do Azure.  
![Contas de armazenamento](./media/security-azure-log-integration-get-started/storage-account.jpg) </br></br>
   6. Observe que há algumas opções em contas de armazenamento. Uma delas é **Tabelas**. Em **Tabelas**, você deverá ver uma chamada **WADWindowsEventLogsTable**. </br></br>
   ![Contas de armazenamento](./media/security-azure-log-integration-get-started/storage-explorer.png) </br>

## <a name="integrate-azure-diagnostic-logging"></a>Integrar o log de Diagnóstico do Azure
Nesta etapa, você irá configurar máquina Olá executando Olá integração do Azure Log serviço tooconnect toohello conta de armazenamento que contém os arquivos de log hello.
toocomplete nesta etapa, precisaremos de algumas coisas com antecedência.  
* **FriendlyNameForSource:** este é um nome amigável que você pode aplicar toohello conta de armazenamento que você configurou informações de toostore de máquina virtual de saudação do diagnóstico do Azure
* **StorageAccountName:** esse é nome Olá Olá da conta de armazenamento que você especificou quando configurou o diagnóstico do Azure.  
* **Chave de armazenamento:** esta é a chave de armazenamento de Olá Olá conta de armazenamento a armazenamento Olá informações de diagnóstico do Azure para esta máquina virtual.  

Execute Olá chave de armazenamento de saudação de tooobtain as etapas a seguir:
 1. Procurar toohello [portal do Azure](http://portal.azure.com).
 2. No painel de navegação de saudação do hello Azure console, role toohello inferior e clique em **mais serviços.**

 ![Mais serviços](./media/security-azure-log-integration-get-started/more-services.png)
 3. Digite **armazenamento** em Olá **filtro** caixa de texto. Clique em **Contas de armazenamento** (isso será exibido depois que você inserir **Armazenamento**)

   ![caixa de filtro](./media/security-azure-log-integration-get-started/filter.png)
 4. Será exibida uma lista de contas de armazenamento, clique duas vezes na conta de saudação que você atribuiu tooLog armazenamento.

   ![lista de contas de armazenamento](./media/security-azure-log-integration-get-started/storage-accounts.png)
 5. Clique em **chaves de acesso** em Olá **configurações** seção.

  ![teclas de acesso](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 6. Cópia **key1** e colocá-la em um local seguro que você pode acessar para a próxima etapa de saudação.

   ![duas chaves de acesso](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 7. No servidor de saudação que você instalou a integração de Log do Azure, abra um Prompt de comando com privilégios elevados (Observe que estamos usando uma janela de Prompt de comando com privilégios elevados aqui, não um console do PowerShell com privilégios elevados).
 8. Navegue muito**c:\Program Files\Microsoft Azure Log integração**
 9. Execute o ``Azlog source add <FriendlyNameForTheSource> WAD <StorageAccountName> <StorageKey> `` </br> Por exemplo ``Azlog source add Azlogtest WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==`` se quiser Olá tooshow de ID de assinatura para cima no evento Olá XML, acrescente o nome amigável da saudação assinatura ID toohello: ``Azlog source add <FriendlyNameForTheSource>.<SubscriptionID> WAD <StorageAccountName> <StorageKey>`` ou, por exemplo,``Azlog source add Azlogtest.YourSubscriptionID WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==``

>[!NOTE]  
Aguardar até too60 minutos, em seguida, exibir eventos de saudação que são extraídos da conta de armazenamento de saudação. tooview, abra **Visualizador de eventos > Logs do Windows > eventos encaminhados** em Olá Azlog integrador.

Aqui você pode ver um vídeo ultrapassou etapas Olá coberto acima.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Enable-Diagnostics-and-Storage/player]


## <a name="what-if-data-is-not-showing-up-in-hello-forwarded-events-folder"></a>Se dados não estão aparecendo na pasta de eventos encaminhados Olá?
Se depois de uma hora dados não estão aparecendo no hello **eventos encaminhados** pasta, em seguida:

1. Serviço Olá máquinas em execução Olá integração de Log do Azure e confirme se ele pode acessar o Azure. tootest conectividade, tente tooopen Olá [portal do Azure](http://portal.azure.com) de navegador hello.
2. Certifique-se de conta de usuário de saudação **Azlog** tem permissão de gravação na pasta Olá **users\Azlog**.
  <ol type="a">
   <li>Abra o **Windows Explorer** </li>
  <li> Navegue muito**c:\users** </li>
  <li> Clique com o botão direito do mouse em **c:\users\Azlog** </li>
  <li> Clique em **Segurança**  </li>
  <li> Clique em **Service\Azlog NT** e verificar permissões Olá conta hello. Se conta hello está ausente neste guia ou se as permissões apropriadas Olá não estão atualmente mostrando pode conceder direitos de conta Olá nesta guia.</li>
  </ol>
3.Tornar-se de conta de armazenamento Olá adicionado no comando Olá **adicionar fonte Azlog** será listado quando você executar o comando Olá **lista de origem Azlog**.
4. Vá muito**Visualizador de eventos > Logs do Windows > aplicativo** toosee se houver erros relatados pela integração do Azure log hello.


Se você tiver algum problema durante a saudação de instalação e configuração, abra um [solicitação de suporte](../azure-supportability/how-to-create-azure-support-request.md), selecione **Log integração** como serviço Olá para o qual você está solicitando suporte.

Outra opção de suporte é hello [Fórum do MSDN de integração do Azure Log](https://social.msdn.microsoft.com/Forums/home?forum=AzureLogIntegration). Aqui comunidade Olá pode dar suporte entre si com perguntas, respostas, dicas e truques sobre como tooget hello mais fora da integração de Log do Azure. Além disso, a equipe de integração do Azure Log Olá monitora este fórum e ajudará sempre que possível.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre a integração de Log do Azure, consulte Olá documentos a seguir:

* [Integração de log do Microsoft Azure para os logs do Azure](https://www.microsoft.com/download/details.aspx?id=53324) – visite o Centro de Download para obter os detalhes, os requisitos de sistema e as instruções de instalação da integração de log do Azure.
* [Integração do log de Introdução tooAzure](security-azure-log-integration-overview.md) – este documento apresenta a integração do registro tooAzure, seus principais recursos e como ele funciona.
* [Etapas de configuração de parceiro](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – esta postagem de blog mostra como tooconfigure Azure log toowork integração com soluções de parceiros Splunk, HP ArcSight e IBM QRadar. Este é nosso atual orientação sobre como tooconfigure Olá componentes SIEM. Primeiro, entre em contato com seu fornecedor do SIEM para obter detalhes adicionais.
* [Perguntas frequentes sobre o log de integração do Azure](security-azure-log-integration-faq.md) – encontre as respostas para as perguntas frequentes sobre a integração de log do Azure.
* [Integração Central de segurança do log de alertas com o Azure Integration](../security-center/security-center-integrating-alerts-with-log-integration.md) – este documento mostra como alertas da Central de segurança toosync, juntamente com coletados pelo diagnóstico do Azure e Logs de atividade do Azure, com a análise de log de eventos de segurança de máquina virtual ou solução SIEM.
* [Novos recursos de diagnóstico do Azure e os Logs de auditoria do Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) – esta postagem de blog apresenta tooAzure os Logs de auditoria e outros recursos que ajudarão a obtém ideias sobre operações de saudação de seus recursos do Azure.
