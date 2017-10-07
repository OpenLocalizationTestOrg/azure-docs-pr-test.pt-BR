---
title: "aaaStorSimple administração do Gerenciador de serviço | Microsoft Docs"
description: "Saiba como toomanage Olá de seu dispositivo StorSimple usando o serviço StorSimple Manager no hello portal clássico do Azure."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2586582e-d85c-42e1-afb3-be734c1c0461
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 695ebbb785590a0e3d6de4c73125f65b16dcb776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooadminister-your-storsimple-device"></a>Usar tooadminister de serviço do StorSimple Manager Olá seu dispositivo StorSimple
## <a name="overview"></a>Visão geral
Este artigo descreve a interface do serviço StorSimple Manager hello, incluindo como tooconnect tooit, Olá várias opções disponíveis e links de fluxos de trabalho específicos do toohello que podem ser executados por meio desta interface do usuário. Este guia é aplicável tooboth; Olá StorSimple físico e o dispositivo virtual hello.

Neste artigo, você aprenderá:

* Conectar-se o serviço de Gerenciador de tooStorSimple
* Navegue Olá UI Gerenciador do StorSimple
* Administrar seu dispositivo StorSimple por meio de saudação serviço StorSimple Manager

## <a name="connect-toostorsimple-manager-service"></a>Conectar-se o serviço de Gerenciador de tooStorSimple
Olá serviço StorSimple Manager é executado no Microsoft Azure e conecta dispositivos de StorSimple toomultiple. Usar um portal clássico central do Microsoft Azure em execução em um navegador toomanage esses dispositivos. tooconnect toohello o serviço StorSimple Manager, Olá a seguir.

#### <a name="tooconnect-toohello-service"></a>serviço de toohello tooconnect
1. Navegue muito[https://manage.windowsazure.com/](https://manage.windowsazure.com/).
2. Usando suas credenciais de conta da Microsoft, faça logon no portal clássico do Microsoft Azure toohello (localizado na saudação de superior direita do painel de saudação).
3. Role para baixo Olá deixado o serviço navegação painel tooaccess Olá StorSimple Manager.

## <a name="navigate-storsimple-manager-service-ui"></a>Navegar para a interface do usuário do StorSimple Manager
Olá a hierarquia de navegação para o serviço StorSimple Manager Olá que interface do usuário é mostrado no Olá a tabela a seguir.

* **Gerenciador de StorSimple** página de aterrissagem usa dispositivos de tooall aplicável de páginas de nível de serviço toohello da interface do usuário dentro de um serviço.
* **Dispositivos** página leva toohello nível do dispositivo da interface do usuário páginas tooa aplicável específica do dispositivo.
* **Contêineres de volume** página usa página de volume toohello que mostra todos os volumes de saudação associados a um dispositivo.

#### <a name="storsimple-manager-service-navigational-hierarchy"></a>Hierarquia de navegação do serviço StorSimple Manager
| Página de aterrisagem | Páginas de nível de serviço | Páginas de nível de dispositivo | Páginas de nível de dispositivo |
| --- | --- | --- | --- |
| Serviço StorSimple Manager |Painel de serviço |Painel do dispositivo | |
| Dispositivos → |Monitoramento | | |
| Catálogo de backup |Contêineres de volume→ |Volumes | |
| Configurar (Serviço) |Políticas de backup | | |
| Trabalhos |Configurar (Dispositivo) | | |
| Alertas |Manutenção | | |

![Vídeo disponível](./media/storsimple-manager-service-administration/Video_icon.png) **Vídeo disponível**

Clique em toowatch um vídeo que orienta você por meio da interface de usuário do serviço do StorSimple Manager Olá, [aqui](https://azure.microsoft.com/documentation/videos/storsimple-manager-service-overview/).

## <a name="administer-storsimple-device-using-storsimple-manager-service"></a>Administrar o dispositivo StorSimple por meio do serviço StorSimple Manager
Olá tabela a seguir mostra um resumo de todas as tarefas comuns de gerenciamento hello e fluxos de trabalho complexos que podem ser executados em Olá serviço StorSimple Manager da interface do usuário. Essas tarefas são organizadas com base nas páginas de interface do usuário Olá no qual elas foram iniciadas.

Para obter mais informações sobre cada fluxo de trabalho, clique em procedimento de saudação apropriado na tabela de saudação.

#### <a name="storsimple-manager-workflows"></a>Fluxos de trabalho do StorSimple Manager
| Se você deseja toodo... | Acesse a página de interface do usuário toothis... | Utilize este procedimento. |
| --- | --- | --- |
| Criar um serviço</br>Excluir um serviço</br>Obter a chave de registro do serviço</br>Regenerar chave de registro do serviço |Serviço StorSimple Manager |[Implantar um serviço StorSimple Manager](storsimple-manage-service.md) |
| Alterar a chave de criptografia de dados de serviço Olá</br>Exibir logs de operação de saudação |Serviço StorSimple Manager → Painel |[Use o painel do serviço StorSimple Manager Olá](storsimple-service-dashboard.md) |
| Desativar um dispositivo</br>Excluir um dispositivo |Serviço StorSimple Manager → Dispositivos |[Desativar ou excluir um dispositivo](storsimple-deactivate-and-delete-device.md) |
| Saiba mais sobre o failover de dispositivo e a recuperação de desastres</br>Dispositivo físico de tooa de failover</br>Dispositivo virtual do failover tooa</br>BCDR (recuperação de desastre de continuidade de negócios) |Serviço StorSimple Manager → Dispositivos |[Failover e recuperação de desastres para o seu dispositivo StorSimple](storsimple-device-failover-disaster-recovery.md) |
| Lista de backups para um volume</br>Selecione um conjunto de backup</br>Excluir um conjunto de backup |Serviço StorSimple Manager → Catálogo de backup |[Gerenciar backups](storsimple-manage-backup-catalog.md) |
| Clonar um volume |Serviço StorSimple Manager → Catálogo de backup |[Clonar um volume](storsimple-clone-volume.md) |
| Restaurar um conjunto de backup |Serviço StorSimple Manager → Catálogo de backup |[Restaurar um conjunto de backup](storsimple-restore-from-backup-set.md) |
| Sobre contas de armazenamento</br>Adicionar uma conta de armazenamento</br>Editar uma conta de armazenamento</br>Excluir uma conta de armazenamento</br>Rotação chave de contas de armazenamento |Serviço StorSimple Manager → Configurar |[Gerenciar contas de armazenamento](storsimple-manage-storage-accounts.md) |
| Sobre modelos de largura de banda</br>Adicionar um modelo de largura de banda</br>Editar um modelo de largura de banda</br>Excluir um modelo de largura de banda</br>Usar um modelo de largura de banda padrão</br>Criar um modelo de largura de banda de dia inteiro que comece em um horário especificado |Serviço StorSimple Manager → Configurar |[Gerenciar modelos de largura de banda](storsimple-manage-bandwidth-templates.md) |
| Sobre os registros de controle de acesso</br>Criar um registro de controle de acesso</br>Editar um registro de controle de acesso</br>Excluir um registro de controle de acesso |Serviço StorSimple Manager → Configurar |[Gerenciar registros de controle de acesso](storsimple-manage-acrs.md) |
| Exibir detalhes do trabalho</br>Cancelar um trabalho |Serviço StorSimple Manager → Trabalhos |[Gerenciar trabalhos](storsimple-manage-jobs.md) |
| Receber notificações de alerta</br>Gerenciar alertas</br>Revisar alertas |Serviço StorSimple Manager → Alertas |[Exibir e gerenciar alertas do StorSimple](storsimple-manage-alerts.md) |
| Exibir iniciadores conectados</br>Localizar o número de série do dispositivo Olá</br>Localizar o IQN de destino Olá |Serviço StorSimple Manager → Dispositivos → Painel |[Use o painel do dispositivo StorSimple Olá](storsimple-device-dashboard.md) |
| Criar gráficos de monitoramento |Serviço StorSimple Manager → Dispositivos → Monitor |[Monitorar o dispositivo StorSimple](storsimple-monitor-device.md) |
| Adicionar um contêiner de volume</br>Modificar um contêiner de volume</br>Excluir um contêiner de volume |Serviço StorSimple Manager → Dispositivos → Contêineres de volume |[Gerenciar contêineres de volume](storsimple-manage-volume-containers.md) |
| Adicionar um volume</br>Modificar um volume</br>Colocar um volume offline</br>Excluir um volume</br>Monitorar um volume |Serviço StorSimple Manager → Dispositivos → Contêineres de volume → Volumes |[Gerenciar volumes](storsimple-manage-volumes.md) |
| Modificar as configurações de dispositivo</br>Modificar as configurações de tempo</br>Modificar as configurações de DNS.md</br>Configurar interfaces de rede |Serviço StorSimple Manager → Dispositivos → Configurar |[Modificar a configuração do dispositivo para seu dispositivo StorSimple](storsimple-modify-device-config.md) |
| Exibir configurações de proxy Web |Serviço StorSimple Manager → Dispositivos → Configurar |[Configurar o proxy Web para o seu dispositivo](storsimple-configure-web-proxy.md) |
| Modificar senha de administrador do dispositivo</br>Modificar senha do StorSimple Snapshot Manager |Serviço StorSimple Manager → Dispositivos → Configurar |[Alterar senhas de StorSimple](storsimple-change-passwords.md) |
| Configurar o gerenciamento remoto |Serviço StorSimple Manager → Dispositivos → Configurar |[Conectar-se remotamente o dispositivo StorSimple tooyour](storsimple-remote-connect.md) |
| Definição de configurações de alerta |Serviço StorSimple Manager → Dispositivos → Configurar |[Exibir e gerenciar alertas do StorSimple](storsimple-manage-alerts.md) |
| Configure o CHAP para o seu dispositivo StorSimple |Serviço StorSimple Manager → Dispositivos → Configurar |[Configure o CHAP para o seu dispositivo StorSimple](storsimple-configure-chap.md) |
| Adicionar uma política de backup</br>Adicionar ou modificar um agendamento</br>Excluir uma política de backup</br>Fazer um backup manual</br>Criar uma política de backup personalizada com vários volumes e agendamentos |Serviço StorSimple Manager → Dispositivos → Políticas de backup |[Gerenciar políticas de backup](storsimple-manage-backup-policies.md) |
| Parar controladores do dispositivo</br>Reiniciar os controladores do dispositivo</br>Desligar os controladores do dispositivo</br>Redefinir o dispositivo toofactory padrão</br>(As opções acima são somente para o dispositivo local) |Serviço StorSimple Manager → Dispositivos → Manutenção |[Gerenciar controlador de dispositivo StorSimple](storsimple-manage-device-controller.md) |
| Saiba mais sobre os componentes de hardware StorSimple</br>Monitorar o status de hardware</br>(As opções acima são somente para o dispositivo local) |Serviço StorSimple Manager → Dispositivos → Manutenção |[Componentes de hardware do monitor](storsimple-monitor-hardware-status.md) |
| Criar um pacote de suporte |Serviço StorSimple Manager → Dispositivos → Manutenção |[Criar e gerenciar pacotes de suporte](storsimple-create-manage-support-package.md) |
| Instalar as atualizações do software |Serviço StorSimple Manager → Dispositivos → Manutenção |[Atualizar seu dispositivo](storsimple-update-device.md) |

## <a name="next-steps"></a>Próximas etapas
Se você tiver problemas com a operação diária de saudação do seu dispositivo StorSimple ou com qualquer um de seus componentes de hardware, consulte:

* [Solucionar problemas de um dispositivo operacional](storsimple-troubleshoot-operational-device.md)
* [Usar LEDs indicadores de monitoramento do StorSimple](storsimple-monitoring-indicators.md)

Se você não conseguir resolver problemas de saudação e você precisar toocreate uma solicitação de serviço, consulte muito[entre em contato com o suporte da Microsoft](storsimple-contact-microsoft-support.md).

