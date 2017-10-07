---
title: "interface de usuário do Gerenciador de instantâneos aaaStorSimple | Microsoft Docs"
description: "Descreve a interface de usuário do Gerenciador de instantâneos StorSimple hello e explica como toouse ela trabalhos de backup toomanage e hello catálogo de backup."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: c7d91892-2881-41a2-a7a2-908dc3646493
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.custom: 
ms.openlocfilehash: 865520fdaf1b559714b52b428ad136b084d65c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-user-interface-toomanage-backup-jobs-and-backup-catalog"></a>Use o Gerenciador do StorSimple Snapshot usuário interface toomanage os trabalhos de backup e o catálogo de backup

## <a name="overview"></a>Visão geral
Olá StorSimple Snapshot Manager tem uma interface de usuário intuitiva que você pode usar tootake e gerenciar backups. Este tutorial fornece uma interface do usuário toohello Introdução e, em seguida, explica como toouse componentes hello. Para obter uma descrição detalhada da saudação StorSimple Snapshot Manager, consulte [o que é StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md)

### <a name="console-description"></a>Descrição do console
usuário de saudação tooview interface, clique no ícone do Gerenciador de instantâneos StorSimple Olá na área de trabalho. janela de console Olá for exibida, conforme mostrado na ilustração a seguir de saudação.

![Painéis do Gerenciador de instantâneos do StorSimple](./media/storsimple-use-snapshot-manager/HCS_SSM_gui_panes.png)

janela de saudação do console possui cinco elementos principais. Clique o link apropriado de saudação para obter uma descrição completa de cada elemento.

* [Barra de menus](#menu-bar) 
* [Barra de ferramentas](#tool-bar) 
* [Painel Escopo](#scope-pane) 
* [Painel Resultados](#results-pane) 
* [Painel Ações](#actions-pane) 

Além disso, a saudação dá suporte ao Gerenciador de instantâneos StorSimple [navegação e um número de atalhos de teclado](#keyboard-navigation-and-shortcuts).

### <a name="console-accessibility"></a>Acessibilidade do console
interface de usuário do Gerenciador de instantâneos StorSimple Olá dá suporte a recursos de acessibilidade do hello fornecidos pelo sistema de operacional do Windows hello e Olá Microsoft Management Console (MMC), bem como alguns atalhos de teclado do Gerenciador de instantâneos do StorSimple específico. 

* Para obter uma descrição dos recursos de acessibilidade do Windows hello, ir muito[atalhos de teclado do Windows](https://support.microsoft.com/kb/126449). 
* Para obter uma descrição dos recursos de acessibilidade do MMC hello, ir muito[acessibilidade do MMC 3.0](https://technet.microsoft.com/library/cc766075.aspx)
* Para obter uma descrição dos recursos de acessibilidade do Gerenciador de instantâneos StorSimple hello, ir muito[navegação e atalhos de teclado](#keyboard-navigation-and-shortcuts).

## <a name="menu-bar"></a>Barra de menus
saudação de barra de menus na parte superior de saudação da janela do console Olá contém [arquivo](#file-menu), [ação](#action-menu), [exibição](#view-menu), [Favoritos](#favorites-menu), [janela ](#window-menu), e [ajuda](#help-menu) menus.

Clique em qualquer item na toosee barra de menu Olá uma lista de comandos disponíveis nesse menu. Olá, exemplo a seguir mostra Olá **exibição** menu selecionado na barra de menus do hello.

![Menu de Exibição selecionado](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png)

### <a name="file-menu"></a>Menu Arquivo
Olá **arquivo** menu contém comandos padrão do Microsoft Management Console (MMC).

#### <a name="menu-access"></a>Acesso ao menu
Olá tooview **arquivo** menu, clique em **arquivo** na barra de menus do hello. Olá menu a seguir é exibida.

![Menu Arquivo do StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_FileMenu.png) 

#### <a name="menu-description"></a>Descrição do menu
Olá tabela a seguir descreve os itens que aparecem no hello **arquivo** menu.

| Item de menu | Descrição |
|:--- |:--- |
| Novo |Clique em **novo** toocreate um novo console com base em Olá StorSimple Snapshot Manager. |
| Aberto |Clique em **abrir** tooopen um console existente. |
| Salvar |Clique em **salvar** console atual do toosave hello. |
| Salvar como |Clique em **Salvar como** toocreate uma nova instância do console atual Olá renomeada. Saudação de uso **Salvar como** opção toocustomize um modo de exibição e salvá-lo para recuperação posterior. Por exemplo, você poderia criar Gerenciador de instantâneos StorSimple snap-ins servidores toospecific ponto. |
| Adicionar/Remover Snap-in |Clique em **Adicionar/Remover Snap-in** tooadd ou remover snap-ins e tooorganize nós Olá **escopo** painel. Para obter mais informações, vá muito[adicionar, remover e organizar Snap-ins e extensões no MMC 3.0](https://technet.microsoft.com/library/cc722035.aspx). |
| Opções |Clique em **opções** toochange ícone de console hello, especificar modos de acesso do usuário e permissões, ou excluir espaço em disco disponível do console arquivos tooincrease. |
| Lista de caminhos de arquivo |Clique em um caminho na Olá numerada lista tooreopen um arquivo que você abriu recentemente. |
| Sair |Clique em **Exit** tooclose Olá **arquivo** menu. |

### <a name="action-menu"></a>Menu Ação
Saudação de uso **ação** tooselect do menu de ações disponíveis. Olá itens disponíveis tooyou dependem da seleção de saudação feitas no hello **escopo** painel ou **resultados** painel.

#### <a name="menu-access"></a>Acesso ao menu
Olá tooview **ação** menu, siga um destes procedimentos hello:

* Clique com botão direito em Olá um item **escopo** painel ou **resultados** painel.
* Selecione um item no hello **escopo** painel ou **resultados** painel e clique **ação** na barra de menus do hello. 

Por exemplo, se você selecionar o nó superior da saudação em Olá **escopo** painel e, em seguida, clique ou **ação** na barra de menus do hello, hello seguinte menu será exibido.

![Menu Ação do StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_Action_menu.png)

Olá **ações** painel (Olá direita do console de saudação) contém Olá mesma lista de ações como Olá **ação** menu. Além disso, Olá **ações** painel contém Olá **exibição** opções de menu, que permitem que você toocreate uma exibição personalizada de saudação **resultados** painel.

![Painel Ações com o menu Exibição aberto](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

#### <a name="menu-description"></a>Descrição do menu
Olá, a tabela a seguir contém uma lista alfabética das ações do Gerenciador de instantâneos do StorSimple. 

* Olá **ação** coluna lista as ações que podem ser executadas em nós e resultados. 
* Olá **navegação** coluna explica como toodisplay Olá apropriado **ação** menu para que você possa selecionar ação de saudação. Algumas ações aparecem em vários menus **Ação** . Para essas ações, selecione uma **navegação** opção de lista com marcadores de saudação. 
* Olá **descrição** coluna descreve como toouse cada ação Olá **ação** menu ou painel de ações e explica o que ele faz.

> [!NOTE]
> Olá **ações** painel e **ação** menus contêm opções adicionais, como **exibição**, **nova janela a partir daqui**,  **Atualizar**, **exportar lista**, e **ajuda**. Essas opções estão disponíveis como parte de saudação do MMC e não são específica tooStorSimple Gerenciador de instantâneos. tabela de saudação inclui descrições dessas opções.
> 
> 

| Ação | Navegação | Descrição |
|:--- |:--- |:--- |
| Autenticar |Clique em Olá **dispositivos** nó e o direito de um dispositivo no hello **resultados** painel. |Clique em **autenticar** tooenter senha de saudação que você configurou para o dispositivo de saudação. |
| Clone |Expanda **catálogo de Backup**, expanda **instantâneos em nuvem**, clique em um backup com data e, em seguida, selecione um volume na Olá **resultados** painel. |Clique em **Clone** toocreate uma cópia de uma nuvem de instantâneo e armazená-lo em um local que você designar. |
| Configurar um Dispositivo |Saudação de atalho **dispositivos** nó. |Clique em **configurar um dispositivo** tooconfigure um dispositivo único ou vários hosts de Windows dispositivos tooconnect toohello. |
| Criar Política de Backup |Execute um dos seguintes hello:<ul><li>Clique com botão direito do mouse em **Políticas de Backup**.</li><li>Clique ou expanda **Grupos de volumes** e clique com o botão direito do mouse em um grupo de volumes.</li><li>Clique ou expanda **Catálogo de Backup** e clique com o botão direito do mouse em um grupo de volumes.</li></ul> |Clique em **Criar política de Backup** tooconfigure um backup agendado para um grupo de volumes. |
| Criar Grupo de Volumes |Execute um dos seguintes hello:<ul><li>Clique em Olá **Volumes** nó e, em seguida, clique com botão direito um volume no hello **resultados** painel.</li><li>Saudação de atalho **grupos de Volume** nó.</li></ul> |Clique em **criar grupo de Volume** tooassign grupo de volumes de tooa de volumes. |
| Exclusão |Clique em um nó ou resultado (esse item aparece em vários menus de **Ação** e nos painéis de **Ações**.) |Clique em **excluir** toodelete Olá nó ou resultado que você selecionou. Quando for exibida a caixa de diálogo de confirmação de hello, confirme ou cancele a exclusão de saudação. |
| Detalhes |Clique em Olá **dispositivos** nó e, em seguida, clique com botão direito um dispositivo no hello **resultados** painel. |Clique em **detalhes** toosee detalhes de configuração de saudação para um dispositivo. |
| Editar |Clique em **políticas de Backup**e clique em uma política de saudação **resultados** painel. |Clique em **editar** toochange agendamento de backup Olá para um grupo de volumes. |
| Exportar Lista |Clique em um nó ou resultado (esse item aparece em todos os menus de **Ação** e nos painéis de **Ações**.) |Clique em **exportar lista** toosave uma lista em um arquivo de valores separados por vírgulas (CSV). Em seguida, você pode importar esse arquivo para um aplicativo de planilha para análise. |
| Ajuda |Clique em qualquer nó ou resultado. (Esse item aparece em todos os menus de **Ação** e painéis de **Ações**.) |Clique em **ajuda** tooopen ajuda online em uma janela separada do navegador. |
| Nova Janela a Partir Daqui |Clique em um nó ou resultado (esse item aparece em todos os menus de **Ação** e nos painéis de **Ações**.) |Clique em **nova janela a partir daqui** tooopen uma nova janela do Gerenciador de instantâneos do StorSimple. |
| Atualizar |Clique em um nó ou resultado (esse item aparece em todos os menus de **Ação** e nos painéis de **Ações**.) |Clique em **atualização** janela de Gerenciador de instantâneos StorSimple tooupdate Olá exibido atualmente. |
| Atualizar Dispositivo |Clique em Olá **dispositivos** nó e o direito de um dispositivo no hello **resultados** painel. |Clique em **atualizar dispositivo** toosynchronize um dispositivo conectado específico com o Gerenciador de instantâneos do StorSimple. |
| Atualizar Dispositivos |Saudação de atalho **dispositivos** nó. |Clique em **atualizar dispositivos** toosynchronize sua lista de dispositivos conectados com o Gerenciador de instantâneos do StorSimple. |
| Examinar volumes novamente |Saudação de atalho **Volumes** nó. |Clique em **examinar volumes novamente** tooupdate Olá lista de volumes exibida no hello **resultados** painel. |
| Restaurar |Expanda **Catálogo de Backup**, expanda um grupo de volumes, expanda **Instantâneos Locais** ou **Instantâneos em Nuvem** e clique com o botão direito do mouse em um backup. |Clique em **restaurar** tooreplace Olá atual grupo dados do volume com dados de saudação do backup selecionado hello. |
| Fazer Backup |Execute um dos seguintes hello:<ul><li>Expanda **Grupos de volumes** e clique com o botão direito do mouse em um grupo de volumes.</li><li>Expanda **Catálogo de Backup** e clique com o botão direito do mouse em um grupo de volumes.</li></ul> |Clique em **fazer Backup** toostart imediatamente um trabalho de backup. |
| Alternar Exibição de Importações |Com o botão direito Olá nó superior Olá **escopo** painel (Olá **StorSimple Snapshot Manager** nó nos exemplos de saudação). |Clique em **alternar a exibição das importações** tooshow ou ocultar grupos de volume hello e backups associados que foram importados do hello painel de serviço do Gerenciador de dispositivos do StorSimple. |

### <a name="view-menu"></a>Menu Exibir
Saudação de uso **exibição** menu toocreate uma exibição personalizada de saudação **resultados** conteúdo do painel. Olá **exibição** menu contém **Adicionar/remover colunas** e **personalizar** opções.

#### <a name="menu-access"></a>Acesso ao menu
Você pode acessar Olá **exibição** menu na barra de menus do hello, ou em Olá **ações** painel.

![Menu Exibir do StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png) 

#### <a name="menu-description"></a>Descrição do menu
Olá tabela a seguir descreve os itens que aparecem no hello **exibição** menu.

| Item de menu | Descrição |
|:--- |:--- |
| Adicionar/Remover Colunas |Clique em **Adicionar/remover colunas** tooadd ou remover colunas em Olá **resultados** painel. |
| Personalizar |Clique em **personalizar** tooshow ou ocultar itens na janela de console do Gerenciador de instantâneos StorSimple hello. |

### <a name="favorites-menu"></a>Menu Favoritos
Use Olá **Favoritos** menu tooadd, remover e organizar exibições de página e as tarefas que você usa com frequência. 

#### <a name="menu-access"></a>Acesso ao menu
Você pode acessar Olá **Favoritos** menu na barra de menus do hello.

![Menu Favoritos do StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_FavoritesMenu.png)

#### <a name="menu-description"></a>Descrição do menu
Olá tabela a seguir descreve os itens que aparecem no hello **Favoritos** menu.

| Item de menu | Descrição |
|:--- |:--- |
| Adicionar tooFavorites |Clique em **adicionar tooFavorites** tooadd Olá atual tooyour lista de exibição de favoritos. |
| Organizar Favoritos |Clique em **Organizar Favoritos** tooorganize conteúdo de saudação da pasta Favoritos. |

### <a name="window-menu"></a>Menu Janela
Saudação de uso **janela** menu tooadd e reorganizar StorSimple Snapshot Manager janelas do console.

#### <a name="menu-access"></a>Acesso ao menu
Você pode acessar Olá **janela** menu na barra de menus do hello.

![Menu Janela do StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_WindowMenu.png)

lista numerada de saudação na parte inferior de saudação do menu Olá mostra Olá janelas que estão atualmente abertas. Clique em qualquer janela na janela lista toobring Olá em primeiro plano da saudação. 

#### <a name="menu-description"></a>Descrição do menu
Olá tabela a seguir descreve Olá itens que aparecem no menu da janela de saudação.

| Item de menu | Descrição |
|:--- |:--- |
| Nova Janela |Clique em **nova janela** tooopen uma nova janela de console (na janela existente do adição toohello). |
| Em cascata |Clique em **Cascade** toodisplay janelas de console abertas Olá em cascata. |
| Lado a lado horizontalmente |Clique em **lado a lado horizontalmente** toodisplay janelas de console abertas Olá em um formato lado a lado (ou grade). |
| Organizar Ícones |Se você tiver vários console windows abrir e dispersos em sua área de trabalho, minimize-as e, em seguida, clique em **organizar ícones** tooarrange-los em uma linha horizontal na parte inferior da saudação da tela. |

### <a name="help-menu"></a>Menu Ajuda
Saudação de uso **ajuda** menu tooview ajuda online disponível para o Gerenciador de instantâneos do StorSimple e hello MMC. Você também pode exibir informações sobre Olá MMC e Gerenciador de instantâneos StorSimple versões de software que estão atualmente instalados no seu sistema. 

Você pode acessar Olá **ajuda** menu na barra de menus do hello. Você também pode acessar os tópicos de Ajuda do Gerenciador de instantâneos do StorSimple da saudação **ações** painel.

![Menu Ajuda do StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpMenu.png)

#### <a name="menu-description"></a>Descrição do menu
Olá a tabela a seguir descreve os itens que aparecem no menu Ajuda do hello.

| Item de menu | Descrição |
|:--- |:--- |
| Ajuda no StorSimple Snapshot Manager |Clique em **ajuda no Gerenciador de instantâneos do StorSimple** tooopen StorSimple Snapshot Manager ajuda em uma janela separada. |
| Tópicos de Ajuda |Clique em **tópicos da Ajuda** tooopen ajuda online do MMC em uma janela separada. |
| Site do TechCenter |Clique em **Site do TechCenter** tooopen Olá Microsoft TechNet Tech Center home página em uma janela separada. |
| No Console de Gerenciamento Microsoft |Clique em **sobre o Console de gerenciamento Microsoft** toosee Olá de qual versão do Console de gerenciamento Microsoft está instalado em seu sistema. |
| Sobre o StorSimple Snapshot Manager |Clique em **sobre o Gerenciador de instantâneos do StorSimple** toosee qual versão do snap-in hello está instalada no sistema. |

## <a name="tool-bar"></a>Barra de ferramentas
barra de ferramentas Hello, localizada abaixo da barra de menus Olá, contém ícones de tarefa e navegação. Cada ícone é uma tarefa específica de tooa de atalho.

### <a name="icon-descriptions"></a>Descrições dos ícones
Olá tabela a seguir descreve os ícones de saudação que aparecem na barra de ferramentas de saudação. 

| ícone | Descrição |
|:--- |:--- |
| ![Seta para a esquerda](./media/storsimple-use-snapshot-manager/HCS_SSM_LeftArrow.png) |Clique em Olá seta para a esquerda ícone tooreturn toohello página anterior. |
| ![Seta para a direita](./media/storsimple-use-snapshot-manager/HCS_SSM_RightArrow.png) |Clique em Olá seta para a direita toogo toohello próxima página (se Olá seta for cinza, Olá ação ficará indisponível). |
| ![Ícone para cima](./media/storsimple-use-snapshot-manager/HCS_SSM_Up.png) |Clique Olá backup toogo ícone um nível acima na árvore de console hello (Olá **escopo** painel). |
| ![Mostrar/ocultar árvore de console](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowConsoleTree.png) |Clique em Olá Mostrar/ocultar console árvore ícone tooshow ou ocultar Olá **escopo** painel. |
| ![Exportar Lista](./media/storsimple-use-snapshot-manager/HCS_SSM_ExportListIcon.png) |Clique em Olá exportar lista ícone tooexport um arquivo CSV tooa de lista que você especificar. |
| ![Ícone de ajuda](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpIcon.png) |Clique em Olá ajuda ícone tooopen um tópico de Ajuda online do MMC. |
| ![Mostrar/ocultar painel de Ações](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowAction.png) |Clique em Mostrar/ocultar Olá **ações** Olá de tooshow ou ocultar ícone painel **ações** painel. |

## <a name="scope-pane"></a>Painel Escopo
Olá **escopo** painel é painel mais à esquerda Olá Olá UI StorSimple Snapshot Manager. Ele contém a árvore de console (ou nó) do hello e é o mecanismo de navegação principal Olá para o Gerenciador de instantâneos do StorSimple. 

### <a name="scope-pane-structure"></a>Estrutura do painel Escopo
Olá **escopo** painel contém uma série de objetos clicáveis (nós) organizada em uma estrutura de árvore. 

![Painel Escopo](./media/storsimple-use-snapshot-manager/HCS_SSM_Scope_pane.png) 

* tooexpand ou recolher um nó, clique em nome de nó do hello seta ícone próximo toohello.
* status de saudação tooview ou conteúdo de um nó, clique em nome do nó hello. informações de saudação aparecem no hello **resultados** painel. 

Olá **escopo** painel contém Olá nós a seguir: 

* [Nó Dispositivos](#devices-node) 
* [Nó Volumes](#volumes-node) 
* [Nó Grupos de Volumes](#volume-groups-node) 
* [Nó Políticas de Backup](#backup-policies-node) 
* [Nó Catálogo de Backups](#backup-catalog-node) 
* [Nó Trabalhos](#jobs-node) 

### <a name="scope-pane-tasks"></a>Tarefas do painel Escopo
Você pode usar o hello **escopo** painel toocomplete uma ação em um nó específico. tooselect uma tarefa, faça o seguinte de saudação:

* Nó hello e, em seguida, selecione tarefa Olá menu Olá que aparece.
* Clique no nó hello e, em seguida, clique em **ação** na barra de menus do hello. Selecione a tarefa de saudação de menu Olá que aparece.
* Clique em nó hello e ação Olá Olá, em seguida, selecione **ações** painel.

Quando você seleciona um nó e usa qualquer um desses métodos toosee uma lista de tarefas, apenas as ações que podem ser executadas nesse nó são mostradas.

### <a name="devices-node"></a>Nó Dispositivos
Olá **dispositivos** nó representa dispositivos de StorSimple hello e dispositivos virtuais StorSimple que estão conectado tooStorSimple Gerenciador de instantâneos. Selecione este nó tooconnect e configurar um dispositivo e importar seus volumes associados, grupos de volumes e cópias de backup existentes. Vários dispositivos podem ser conectados tooa único host.

* nó de saudação tooexpand, clique no ícone de seta Olá lado muito**dispositivos**.
* toosee um menu de ações disponíveis, clique com botão direito Olá **dispositivos** nó ou o botão direito do mouse qualquer um de nós de saudação que aparecem no hello visualização expandida.
* toosee uma lista de dispositivos configurados, clique em **dispositivos** em Olá **escopo** painel. lista de saudação de dispositivos, juntamente com informações sobre cada dispositivo, aparece no hello **resultados** painel.

### <a name="volumes-node"></a>Nó Volumes
Olá **Volumes** nó representa unidades de saudação que correspondem a toohello volumes montados pelo host hello, incluindo os descobertos através de iSCSI e aqueles descobertos através de um dispositivo. Use esta lista de saudação do tooview de nó de volumes disponíveis e atribuir volumes individuais toovolume grupos.

* nó de saudação tooexpand, clique no ícone de seta Olá lado muito**Volumes**.
* toosee um menu de ações disponíveis, clique com botão direito Olá **Volumes** nó ou o botão direito do mouse qualquer um de nós de saudação que aparecem no hello visualização expandida.
* toosee uma lista de volumes, clique em **Volumes** em Olá **escopo** painel. lista de saudação de volumes, juntamente com informações sobre cada volume, aparece no hello **resultados** painel.

### <a name="volume-groups-node"></a>Nó Grupos de Volumes
Grupos de volumes também são conhecidos como grupos de consistência. Cada grupo de volume é um conjunto de volumes relacionados ao aplicativo que ajuda a consistência do aplicativo tooensure durante operações de backup. Saudação de uso **grupos de Volume** nó tooconfigure esses grupos e backups interativos tootake ou criar agendas de backup. 

* nó de saudação tooexpand, clique no ícone de seta Olá lado muito**grupos de Volume**.
* toosee um menu de ações disponíveis, clique com botão direito Olá **grupos de Volume** nó ou o botão direito do mouse qualquer um de nós de saudação que aparecem no hello visualização expandida.
* toosee uma lista de grupos de volumes, clique em **grupos de Volume** em Olá **escopo** painel. lista de saudação de grupos de volume, junto com informações sobre cada grupo de volume, aparece no hello **resultados** painel.

### <a name="backup-policies-node"></a>Nó Políticas de Backup
Políticas de backup são agendas de trabalhos para instantâneos locais e na nuvem. Saudação de uso **políticas de Backup** toospecify nó frequência um backup é criado e quanto tempo um backup deve ser mantido. 

* nó de saudação tooexpand, clique no ícone de seta Olá lado muito**políticas de Backup**.
* toosee um menu de ações disponíveis, clique com botão direito Olá **políticas de Backup** nó ou o botão direito do mouse qualquer um de nós de saudação que aparecem no hello visualização expandida.
* toosee uma lista de políticas de backup, clique em **políticas de Backup** em Olá **escopo** painel. lista de saudação de políticas de backup, junto com informações sobre cada política aparece no hello **resultados** painel.

> [!NOTE]
> Você pode manter um máximo de 64 backups.


### <a name="backup-catalog-node"></a>Nó Catálogo de Backups
Olá **catálogo de Backup** nó contém listas de locais e fora de backups de volumes do StorSimple do Azure. Este nó é organizado por grupo de volume e cada contêiner de grupo de volume contém estruturas separadas para instantâneos locais (Olá **instantâneo Local**nó s) e instantâneos em nuvem (Olá **instantâneos em nuvem** nó ). Quando expandido, cada contêiner de grupo de volume lista todos os backups bem-sucedidos Olá foram realizados interativamente ou por uma política configurada.

* nó de saudação tooexpand, clique no ícone de seta Olá lado muito**catálogo de Backup**.
* toosee um menu de ações disponíveis, clique com botão direito Olá **catálogo de Backup** nó ou o botão direito do mouse qualquer um de nós de saudação que aparecem no hello visualização expandida.
* toosee uma lista de instantâneos de backup, clique em **catálogo de Backup** em Olá **escopo** painel. lista de saudação de instantâneos, juntamente com informações sobre cada instantâneo, aparece no hello **resultados** painel.

### <a name="local-snapshots-node"></a>Nó Instantâneos Locais
Olá **instantâneos locais** nó da lista de instantâneos locais para um grupo de volumes específico. Olá nó está localizado em Olá **catálogo de Backup** nó Olá **escopo** painel. Os instantâneos locais são cópias point-in-time de dados de volume que estão armazenados no dispositivo Azure StorSimple de saudação. Normalmente, esse tipo de backup pode ser criado e restaurado rapidamente. Você pode usar um instantâneo local como faria com uma cópia de backup local.

* nó de saudação tooexpand, clique no ícone de seta Olá lado muito**instantâneos locais**.
* toosee um menu de ações disponíveis, clique com botão direito Olá **instantâneos locais** nó ou o botão direito do mouse qualquer um de nós de saudação que aparecem no hello visualização expandida.
* toosee uma lista de instantâneos locais, clique em **instantâneos locais** em Olá **escopo** painel. lista de saudação de instantâneos, juntamente com informações sobre cada instantâneo, aparece no hello **resultados** painel.

### <a name="cloud-snapshots-node"></a>Nó Instantâneos de Nuvem
Olá **instantâneos em nuvem** nó da lista de instantâneos na nuvem para um grupo de volumes específico. Olá nó está localizado em Olá **catálogo de Backup** nó Olá **escopo** painel. Instantâneos de nuvem são cópias point-in-time de dados de volume que estão armazenados na nuvem hello. Um instantâneo de nuvem é equivalente instantâneo tooa replicado em um sistema de armazenamento externo, diferentes. Instantâneos de nuvem são particularmente úteis em cenários de recuperação de desastres.

* nó de saudação tooexpand, clique no ícone de seta Olá lado muito**instantâneos em nuvem**.
* toosee um menu de ações disponíveis, clique com botão direito Olá **instantâneos em nuvem** nó ou o botão direito do mouse qualquer um de nós de saudação que aparecem no hello visualização expandida.
* toosee uma lista de instantâneos de nuvem, clique em **instantâneos em nuvem** em Olá **escopo** painel. lista de saudação de instantâneos, juntamente com informações sobre cada instantâneo, aparece no hello **resultados** painel.

### <a name="jobs-node"></a>Nó Trabalhos
Olá **trabalhos** nó contém informações sobre os trabalhos de backup agendados, em execução e concluídos recentemente. 

* nó de saudação tooexpand, clique no ícone de seta Olá lado muito**trabalhos**.
* toosee um menu de ações disponíveis, clique com botão direito Olá **trabalhos** nó ou o botão direito do mouse qualquer um de nós de saudação que aparecem no hello visualização expandida.
* toosee uma lista dos trabalhos agendados, expanda Olá **trabalhos** nó e, em seguida, clique **agendada**. Olá lista de trabalhos configurados anteriormente e informações sobre cada trabalho aparece no hello **resultados** painel. 
* toosee uma lista dos trabalhos concluídos recentemente, expanda Olá **trabalhos** nó e, em seguida, clique **últimas 24 horas**. É exibida uma lista de trabalhos que foram concluídas no hello últimas 24 horas em Olá **resultados** painel. Olá **resultados** painel também contém informações sobre cada trabalho concluído.
* toosee uma lista de trabalhos que estão sendo executados, expanda Olá **trabalhos** nó e, em seguida, clique **executando**. lista de saudação de trabalhos em execução e informações sobre cada trabalho aparece no hello **resultados** painel.

## <a name="results-pane"></a>Painel Resultados
Olá **resultados** painel é painel center Olá Olá UI StorSimple Snapshot Manager. Ele contém listas e informações detalhadas para o nó de saudação selecionado na Olá **escopo** painel.

### <a name="example"></a>Exemplo
Olá toosee exemplo, a seguir clique Olá **grupos de Volume** nó Olá **escopo** painel. Olá **resultados** painel exibe uma lista de grupos de volume com detalhes sobre cada grupo.

![Painel Resultados](./media/storsimple-use-snapshot-manager/HCS_SSM_Results_pane.png) 

Você pode configurar os detalhes de saudação mostrados no hello **resultados** painel: clique de um nó em Olá **escopo** painel, clique em **exibição**e, em seguida, clique em **Adicionar/remover Colunas**.

## <a name="actions-pane"></a>Painel Ações
Olá **ações** painel é Olá direita Olá UI StorSimple Snapshot Manager. Ele contém um menu de operações que você pode executar no nó hello, exibição ou dados que você selecionar no hello **escopo** painel ou **resultados** painel. Olá **ações** painel contém Olá mesmo comandos como Olá **ação** menus estão disponíveis para itens no hello **escopo** painel e **resultados**painel. Para obter uma descrição de cada ação, consulte a tabela Olá Olá **ação** seção do menu.

### <a name="examples"></a>Exemplos
Olá toosee seguindo o exemplo hello **escopo** painel, expanda Olá **trabalhos** nó e clique em **agendada**. Olá **ações** painel exibe as ações disponíveis para Olá Olá **agendada** nó.

![Exemplo de trabalhos agendados do painel Ações](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane.png) 

toosee mais opções, no hello **escopo** painel, expanda Olá **trabalhos** nó, clique em **agendada**e, em seguida, clique em um trabalho agendado em Olá **resultados**painel. Olá **ações** painel exibe as ações disponíveis para o trabalho agendado do hello, Olá, conforme mostrado no exemplo a seguir de saudação.

![Exemplo de ações de trabalho do painel Ações](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

## <a name="keyboard-navigation-and-shortcuts"></a>Navegação por teclado e atalhos
Gerenciador de instantâneos StorSimple permite que os recursos de acessibilidade de saudação do sistema de operacional do Windows hello e hello Microsoft Management Console (MMC). Ele também inclui alguns recursos de navegação do teclado e atalhos específico toohello StorSimple Snapshot Manager, conforme descrito em Olá seções a seguir.

* [Teclas de navegação de teclado](#keyboard-navigation-keys) 
* [Teclas de atalho da barra de menus](#menu-bar-shortcut-keys) 
* [Teclas de atalho do painel Escopo](#scope-pane-shortcut-keys) 

### <a name="keyboard-navigation-keys"></a>Teclas de navegação de teclado
Olá tabela a seguir descreve chaves Olá que você pode usar a interface do usuário toonavigate Olá StorSimple Snapshot Manager. 

| Tecla de navegação | Ação |
|:--- |:--- |
| Seta para baixo |Usar o hello para baixo toomove teclas de seta verticalmente toohello próximo item em um menu ou painel. |
| Digite |Pressione Enter Olá toocomplete com chave uma ação e continue toohello próxima etapa. Por exemplo, você pode pressionar Enter tooselect **próximo**, **Okey**, ou **criar**, e, em seguida, vá toohello próxima etapa em um assistente. |
| Esc |Pressione Olá Esc tooclose chave um menu ou toocancel e fechar uma página. |
| F1 |Pressione tooview chave de F1 de saudação um tópico da Ajuda para a janela ativa no momento da saudação. |
| F5 |Pressione F5 Olá toorefresh com chave um nó. |
| F6 |Pressione Olá F6 chave toomove de saudação **escopo** painel toohello **resultados** painel. |
| F10 |Pressione a barra de menus do hello F10 toogo chave toohello. |
| Tecla de seta para a esquerda |Use Olá deixado toomove teclas de seta horizontal de uma opção anterior toohello da opção menu barra. Quando você move toohello anterior menu item em Olá menu barra, ação hello (ou contexto) para o item anterior da saudação é exibida. |
| Tecla de seta para a direita |Use Olá seta para a direita chave toomove horizontalmente de um menu barra toohello opção ao lado. Quando você move toohello próximo menu item em Olá menu barra, ação hello (ou contexto) para o novo item de saudação é exibida. |
| Tecla TAB |Use Olá guia toomove chave toohello próximo painel no hello console ou toohello próxima seleção ou caixa de texto em uma página. |
| Tecla de seta para cima |Use Olá backup toomove teclas de seta verticalmente toohello o item anterior em um menu ou painel. |

### <a name="menu-bar-shortcut-keys"></a>Teclas de atalho da barra de menus
Olá tabela a seguir descreve combinações de teclas de atalho Olá Olá barra de menus. Depois de você pressionar teclas de atalho hello e Olá menu é aberto, você pode usar as teclas de atalho (Olá teclas sublinhadas no menu de saudação). Para obter mais informações sobre a barra de menus do hello, vá muito[barra de menus](#menu-bar).

| Atalho | Result | Tecla de atalho do menu | Result |
|:--- |:--- |:--- |:--- |
| ALT + F |Olá abre **arquivo** menu. |N |Abre uma nova instância do console. |
|  |O |Olá abre **ferramentas administrativas** página. | |
|  |S |Salva o console do Gerenciador de instantâneos StorSimple hello. | |
|  |Uma |Olá abre **Salvar como** página. | |
|  |M |Olá abre **Adicionar/Remover Snap-in** página. | |
|  |P |Olá abre **opções** página. | |
|  |H |Abre a Ajuda online. | |
| ALT+A |Olá abre **ação** menu. |I |Ativa e desativa a opção de exibição de importação de saudação. |
|  |W |Abre um novo console do StorSimple Snapshot Manager. | |
|  |F |Atualiza o console do Gerenciador de instantâneos StorSimple hello. | |
|  |L |Olá abre **exportar lista** página. | |
|  |H |Abre a Ajuda online. | |
| ALT+V |Olá abre **exibição** menu. |Uma |Olá abre **Adicionar/remover colunas** página. |
|  |U |Olá abre **Personalizar modo de exibição** página. | |
| ALT+O |Olá abre **Favoritos** menu. |Uma |Olá abre **adicionar tooFavorites** página. |
|  |O |Olá abre **Organizar Favoritos** página. | |
| ALT+W |Olá abre **janela** menu. |N |Abre outra janela do StorSimple Snapshot Manager. |
|  |C |Exibe todas as janelas de console abertas em um estilo em cascata. | |
|  |T |Exibe todas as janelas de console abertas em um padrão de grade. | |
|  |I |Organiza os ícones em uma linha horizontal na parte inferior da saudação da tela. | |
| ALT+H |Olá abre **ajuda** menu. |H |Abre a Ajuda online. |
|  |T |Abre a página de web do Microsoft TechNet Tech Center hello. | |
|  |Uma |Olá abre **sobre o Console de gerenciamento Microsoft** página. | |

### <a name="scope-pane-shortcut-keys"></a>Teclas de atalho do painel Escopo
Olá tabelas a seguir mostram atalho Olá combinações de teclas para cada nó no hello **escopo** painel. 

* [Teclas de atalho do nó Dispositivos](#devices-node-shortcut-keys)
* [Teclas de atalho do nó Volumes](#volumes-node-shortcut-keys)
* [Teclas de atalho do nó Grupos de Volumes](#volume-groups-node-shortcut-keys)
* [Teclas de atalho do nó Políticas de Backup](#backup-policies-node-shortcut-keys)
* [Teclas de atalho do nó Catálogo de Backups](#backup-catalog-node-shortcut-keys)
* [Teclas de atalho do nó Trabalhos](#jobs-node-shortcut-keys)

#### <a name="devices-node-shortcut-keys"></a>Teclas de atalho do nó Dispositivos
| Atalho de menu | Result |
|:--- |:--- |
| C |Olá abre **configurar um dispositivo** página. |
| D |Atualiza a lista de saudação de dispositivos e detalhes do dispositivo. |
| V |Olá abre **exibição** menu. |
| W |Abre um novo console do Gerenciador de instantâneos StorSimple voltado Olá **detalhes** nó. |
| F |Atualiza o console do Gerenciador de instantâneos StorSimple hello. |
| L |Olá abre **exportar lista** página. |
| H |Abre a Ajuda online. |

#### <a name="volumes-node-shortcut-keys"></a>Teclas de atalho do nó Volumes
| Atalho de menu | Result |
|:--- |:--- |
| V |Lista de saudação de atualizações de volumes. |
| V (pressione duas vezes) |Olá abre **exibição** menu. |
| W |Abre um novo console do Gerenciador de instantâneos StorSimple voltado Olá **Volumes** nó. |
| F |Atualiza o console do Gerenciador de instantâneos StorSimple hello. |
| L |Olá abre **exportar lista** página. |
| H |Abre a Ajuda online. |

#### <a name="volume-groups-node-shortcut-keys"></a>Teclas de atalho do nó Grupos de Volumes
| Atalho de menu | Result |
|:--- |:--- |
| G |Olá abre **criar um grupo de volumes** página. |
| V |Olá abre **exibição** menu. |
| W |Abre um novo console do Gerenciador de instantâneos StorSimple voltado Olá **grupos de Volume** nó. |
| F |Atualiza o console do Gerenciador de instantâneos StorSimple hello. |
| L |Olá abre **exportar lista** página. |
| H |Abre a Ajuda online. |

#### <a name="backup-policies-node-shortcut-keys"></a>Teclas de atalho do nó Políticas de Backup
| Atalho de menu | Result |
|:--- |:--- |
| B |Olá abre **criar uma política de** página. |
| V |Olá abre **exibição** menu. |
| W |Abre um novo console do Gerenciador de instantâneos StorSimple voltado Olá **grupos de Volume** nó. |
| F |Atualiza o console do Gerenciador de instantâneos StorSimple hello. |
| L |Olá abre * * exportar lista * * página. |
| H |Abre a Ajuda online. |

#### <a name="backup-catalog-node-shortcut-keys"></a>Teclas de atalho do nó Catálogo de Backups
| Atalho de menu | Result |
|:--- |:--- |
| W |Abre um novo console do Gerenciador de instantâneos StorSimple voltado Olá **grupos de Volume** nó. |
| F |Atualiza o console do Gerenciador de instantâneos StorSimple hello. |
| H |Abre a Ajuda online. |

#### <a name="jobs-node-shortcut-keys"></a>Teclas de atalho do nó Trabalhos
| Atalho de menu | Result |
|:--- |:--- |
| V |Olá abre **exibição** menu. |
| W |Abre um novo console do Gerenciador de instantâneos StorSimple voltado Olá **trabalhos** nó. |
| F |Atualiza o console do Gerenciador de instantâneos StorSimple hello. |
| L |Olá abre **exportar lista** página. |
| H |Abre a Ajuda online |

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[usar o Gerenciador de instantâneos StorSimple tooadminister sua solução StorSimple](storsimple-snapshot-manager-admin.md).
* Saiba como muito[usar o Gerenciador de instantâneos StorSimple tooconnect e gerenciar dispositivos](storsimple-snapshot-manager-manage-devices.md).

