---
title: captura de pacote aaaManage com observador de rede do Azure - portal do Azure | Microsoft Docs
description: "Esta página explica como toomanage Olá recurso de captura de pacote do observador de rede usando o portal do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a>Gerenciar capturas de pacote com o observador de rede do Azure usando o portal de saudação

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [API REST do Azure](network-watcher-packet-capture-manage-rest.md)

Captura de pacote do Inspetor de rede permite que você toocreate captura sessões tootrack tráfego tooand de uma máquina virtual. Filtros são fornecidos para Olá tooensure de sessão de captura que somente o tráfego de saudação que você deseja capturar. Captura de pacote ajuda anomalias de rede toodiagnose reativo e proativo. Outros usos incluem a coleta de estatísticas de rede, obtenção de informações de invasões de rede, toodebug cliente-servidor comunicações e muito mais. Sendo tooremotely capaz de captura de pacote de gatilho, esse recurso facilita a carga de saudação da execução de uma captura de pacote e manualmente no computador desejado hello, que economiza tempo.

Este artigo o orienta por Olá diversas tarefas de gerenciamento que estão atualmente disponíveis para captura de pacote.

- [**Iniciar uma captura de pacote**](#start-a-packet-capture)
- [**Parar uma captura de pacote**](#stop-a-packet-capture)
- [**Excluir uma captura de pacote**](#delete-a-packet-capture)
- [**Baixar uma captura de pacote**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Antes de começar

Este artigo pressupõe que você tenha Olá recursos a seguir:

- Uma instância do observador de rede na região Olá deseja toocreate uma captura de pacote
- Uma máquina virtual com o pacote de saudação capturar extensão habilitada.

> [!IMPORTANT]
> A captura de pacotes requer uma extensão da máquina virtual `AzureNetworkWatcherExtension`. Para instalar a extensão de saudação em uma VM do Windows, visite [extensão de máquina virtual do agente do Inspetor de rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para a visita de VM do Linux [extensão de máquina virtual do agente do Inspetor de rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).

### <a name="packet-capture-agent-extension-through-hello-portal"></a>Extensão do agente de captura de pacote por meio do portal Olá

captura de pacote de saudação tooinstall agente da VM por meio do portal hello, navegar tooyour virtual machine, clique em **extensões** > **adicionar** e procure **rede Inspetor de agente para Windows**

![exibição de agentes][agent]

## <a name="packet-capture-overview"></a>visão geral da Captura de Pacotes

Navegue toohello [portal do Azure](https://portal.azure.com) e clique em **rede** > **observador de rede** > **de captura de pacote**

página de visão geral de saudação mostra a que captura de uma lista de todos os pacotes existentes, independentemente do estado de saudação.

> [!NOTE]
> Captura de pacote requer a conta de armazenamento toohello conectividade pela porta 443.

![tela de visão geral da captura de pacotes][1]

## <a name="start-a-packet-capture"></a>Iniciar uma captura de pacotes

Clique em **adicionar** toocreate uma captura de pacote.

Olá propriedades que podem ser definidas em uma captura de pacote são:

**Configurações principais**

- **Assinatura** -este valor é a assinatura de saudação que é usada, uma instância do observador de rede é necessária em cada assinatura.
- **Grupo de recursos** -grupo de recursos de saudação da máquina virtual hello está sendo direcionada.
- **Máquina virtual de destino** -Olá máquina de virtual que está executando a captura de pacote de saudação
- **Nome de captura de pacote** -esse valor é o nome de saudação da captura de pacote de saudação.

**Configuração da captura**

- **Conta de Armazenamento** - Determina se a captura do pacote é salva em uma conta de armazenamento.
- **Arquivo** -determina se uma captura de pacote é salvo localmente na máquina virtual de saudação.
- **Contas de armazenamento** -Olá selecionado captura de pacote de saudação do armazenamento conta toosave no. O local padrão é https://{nome da conta de armazenamento}.blob.core.windows.net/network-watcher-logs/subscriptions/{id assinatura}/resourcegroups/{nome do grupo de recursos}/providers/microsoft.compute/virtualmachines/{nome máquina virtual}/{AA}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap. (Habilitado somente se o **Armazenamento** estiver selecionado)
- **Caminho de arquivo local** -caminho de local de saudação em uma captura de pacote de saudação de toosave de máquina virtual. (Habilitado somente se o **Arquivo** estiver selecionado). Um caminho válido deve ser fornecido
- **Máximo de bytes por pacote** -Olá o número de bytes de cada pacote que são capturadas, todos os bytes são capturados se deixado em branco.
- **Máximo de bytes por sessão** - Total número de bytes que são capturadas, quando o valor de saudação é atingido Olá paradas de captura de pacote.
- **Tempo limite (segundos)** -define um limite de tempo para Olá toostop de captura de pacote. O padrão é 18.000 segundos.

> [!NOTE]
> As contas de armazenamento Premium atualmente não têm suporte para armazenar as capturas de pacotes.

**Filtragem (Opcional)**

- **Protocolo** -Olá toofilter de protocolo para captura de pacote de saudação. os valores disponíveis Olá são TCP, UDP e qualquer.
- **Endereço IP local** -esse valor filtra Olá toopackets de captura de pacote em que o endereço IP local Olá corresponde esse valor de filtro.
- **Porta local** -esse valor filtra Olá toopackets de captura de pacote em que a porta local Olá corresponde esse valor de filtro.
- **Endereço IP remoto** -esse valor filtra Olá toopackets de captura de pacote onde IP remoto Olá corresponde a esse valor de filtro.
- **Porta remota** -esse valor filtra Olá toopackets de captura de pacote em que a porta remota Olá corresponde esse valor de filtro.

> [!NOTE]
> Os valores da porta e do endereço IP podem ser um único valor, um intervalo de valores ou um conjunto. (ou seja, 80-1024 para a porta) Você pode definir quantos filtros quiser.

Depois de preencher valores hello, clique em **Okey** toocreate captura de pacote de saudação.

![criar uma captura de pacotes][2]

Depois de definir o limite de tempo de saudação em captura de pacote de saudação expirou, captura de pacote de saudação será interrompida e pode ser examinada. Manualmente, você pode interromper sessões de captura de pacote hello.

## <a name="delete-a-packet-capture"></a>Excluir uma captura de pacotes

No pacote de saudação capturar o modo de exibição, clique em Olá **menu de contexto** (...) ou o botão direito do mouse e clique em **excluir** toostop captura de pacote de saudação

![excluir uma captura de pacotes][3]

> [!NOTE]
> Excluir uma captura de pacote não exclui o arquivo hello na conta de armazenamento hello.

Você será solicitado tooconfirm deseja toodelete captura de pacote de saudação, clique em **Sim**

![confirmação][4]

## <a name="stop-a-packet-capture"></a>Parar uma captura de pacotes

No pacote de saudação capturar o modo de exibição, clique em Olá **menu de contexto** (...) ou o botão direito do mouse e clique em **parar** toostop captura de pacote de saudação

## <a name="download-a-packet-capture"></a>Baixar um pacote de capturas

Depois de concluído, a sessão de captura de pacote hello captura arquivo é carregado tooblob armazenamento ou tooa local em Olá VM. local de armazenamento de saudação de captura de pacote de saudação é definido no momento da criação da sessão de saudação. Uma ferramenta conveniente tooaccess esses capturar os arquivos salvos tooa conta de armazenamento é o Microsoft Azure Storage Explorer, que pode ser baixado em: http://storageexplorer.com/

Se uma conta de armazenamento for especificada, os arquivos de captura de pacote são salvos tooa conta de armazenamento no hello local a seguir:
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Próximas etapas

Saiba como o pacote tooautomate captura com alertas de máquina Virtual por meio da exibição [criar uma captura de pacote de disparo de alerta](network-watcher-alert-triggered-packet-capture.md)

Localize se determinado tráfego é permitido dentro ou fora de sua VM visitando [Verificar o fluxo do IP](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













