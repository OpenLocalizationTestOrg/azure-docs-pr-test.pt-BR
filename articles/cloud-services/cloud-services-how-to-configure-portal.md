---
title: "aaaHow tooconfigure um serviço de nuvem (portal) | Microsoft Docs"
description: "Saiba como os serviços de nuvem tooconfigure no Azure. Aprenda a configuração do serviço de nuvem tooupdate hello e configurar instâncias de toorole de acesso remoto. Esses exemplos usam Olá portal do Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a>Como os serviços de nuvem tooConfigure
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-how-to-configure-portal.md)
> * [Portal clássico do Azure](cloud-services-how-to-configure.md)
>
>

Você pode definir configurações de hello mais comumente usada para um serviço de nuvem no portal do Azure de saudação. Ou, se desejar tooupdate seus arquivos de configuração diretamente, baixar um tooupdate de arquivo de configuração de serviço e, em seguida, carregar Olá atualizado de arquivo e atualização Olá serviço de nuvem com as alterações de configuração de saudação. De qualquer forma, as atualizações de configuração de saudação são enviados por push tooall instâncias de função.

Você também pode gerenciar instâncias de saudação do funções de serviço de nuvem, ou área de trabalho remota-los.

Azure pode apenas certifique-se de 99,95% de disponibilidade durante a saudação atualizações de configuração se você tem pelo menos duas instâncias de função para cada função. Que permite que uma máquina virtual tooprocess cliente solicitações enquanto outros hello está sendo atualizada. Para obter mais informações, consulte [Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Alterar um serviço de nuvem
Após a abertura Olá [portal do Azure](https://portal.azure.com/), navegar tooyour serviço de nuvem. Daqui, você gerencia muitos aspectos dele.

![Página de configurações](./media/cloud-services-how-to-configure-portal/cloud-service.png)

Olá **configurações** ou **todas as configurações** links abrirá Olá **configurações** folha de onde você pode alterar Olá **propriedades**, alterar Olá **Configuração**, gerenciar Olá **certificados**, instalação **regras de alerta**e gerenciar Olá **usuários** que têm acesso toothis serviço de nuvem.

![Folha de configurações do serviço de nuvem do Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a>Gerenciar versão do SO Convidado

Por padrão, o Azure atualiza periodicamente a convidado toohello mais recente com suporte imagem do sistema operacional em Olá família do sistema operacional que você especificou na sua configuração de serviço (. cscfg), como Windows Server 2016.

Se você precisar tootarget uma versão específica do sistema operacional, você pode defini-lo no hello **configuração** folha.

![Definir versão do SO](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> Escolher uma versão específica do SO desabilita as atualizações automáticas do sistema operacional e torna os patches sua responsabilidade. Você deve garantir que suas instâncias de função estão recebendo atualizações ou você pode expor vulnerabilidades de toosecurity seu aplicativo.

## <a name="monitoring"></a>Monitoramento
Você pode adicionar o serviço de nuvem tooyour alertas. Clique em **Configurações** > **Regras de Alerta** > **Adicionar alerta**.

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

Daqui, você pode configurar um alerta. Com hello **métrica** caixa suspensa, você pode configurar um alerta para Olá seguintes tipos de dados.

* Leitura de disco
* Gravação de disco
* Rede no
* Limite de rede
* Percentual de CPU

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a>Configurar o monitoramento de um bloco de métrica
Em vez de usar **configurações** > **regras de alerta**, você pode clicar em um dos blocos da métrica no Olá Olá **monitoramento** seção Olá **nuvem serviço** folha.

![Monitoramento de Serviço de Nuvem](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

Aqui você pode personalizar Olá gráfico usado com o bloco de saudação ou adicionar uma regra de alerta.

## <a name="reboot-reimage-or-remote-desktop"></a>Reinicializar, refazer imagem ou a área de trabalho remota
Neste momento, você não pode configurar a área de trabalho remota usando Olá **portal do Azure**. No entanto, você pode configurá-lo por meio de saudação [portal clássico do Azure](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), ou por meio [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).

Primeiro, clique na instância de serviço de nuvem hello.

![Instância de Serviço de Nuvem](./media/cloud-services-how-to-configure-portal/cs-instance.png)

De saudação folha que abre, você pode iniciar uma conexão de área de trabalho remota, reinicializar a instância de hello, ou remotamente a instância de saudação de refazer (com uma nova imagem de inicialização).

![Botões de instância de serviço de nuvem](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a>Reconfigurar seu .cscfg
Talvez seja necessário tooreconfigure seu serviço de nuvem por meio de saudação [a configuração de serviço (cscfg)](cloud-services-model-and-package.md#cscfg) arquivo. Primeiro é necessário toodownload o. cscfg do arquivo, modificá-la e carregá-lo.

1. Clique em hello **configurações** ícone ou hello **todas as configurações** link tooopen backup Olá **configurações** folha.

    ![Página de configurações](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. Clique em Olá **configuração** item.

    ![Folha de configuração](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. Clique em Olá **baixar** botão.

    ![Baixar](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. Depois de atualizar o arquivo de configuração de serviço hello, carregar e aplicar as atualizações de configuração de saudação:

    ![Carregar](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. Selecione o arquivo do hello. cscfg e clique em **Okey**.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[implantar um serviço de nuvem](cloud-services-how-to-create-deploy-portal.md).
* Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name-portal.md).
* [Gerenciar seu serviço de nuvem](cloud-services-how-to-manage-portal.md).
* Configurar [certificados SSL](cloud-services-configure-ssl-certificate-portal.md).
