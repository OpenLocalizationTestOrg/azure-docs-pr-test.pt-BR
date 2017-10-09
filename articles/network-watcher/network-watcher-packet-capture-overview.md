---
title: captura de tooPacket aaaIntroduction no Inspetor de rede do Azure | Microsoft Docs
description: "Esta página fornece uma visão geral do recurso de captura de pacote hello observador de rede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a>Captura de pacote toovariable introdução em observador de rede do Azure

Captura de pacote de variável do Inspetor de rede permite que você toocreate pacote captura sessões tootrack tooand de tráfego de uma máquina virtual. Captura de pacote ajuda toodiagnose anomalias na rede ambos os reativa e proactivity. Outros usos incluem a coleta de estatísticas de rede, obtenção de informações de invasões de rede, toodebug cliente-servidor comunicações e muito mais.

A captura de pacote é uma extensão de máquina virtual iniciada remotamente por meio do Observador de Rede. Esse recurso facilita a carga Olá da execução de uma captura de pacote manualmente na máquina virtual Olá desejado, o que economiza tempo. Captura de pacote pode ser acionada por meio do portal de saudação, o PowerShell, CLI ou API REST. Os alertas de Máquina Virtual são um exemplo de como a captura de pacote pode ser disparada. Os filtros são fornecidos para tooensure de sessão de captura Olá você capturar o tráfego que você deseja toomonitor. Os filtros têm base em informações de cinco tuplas (protocolo, endereço IP local, endereço IP remoto, porta local e porta remota). Olá capturado dados são armazenados no disco local hello ou um blob de armazenamento. Há um limite de 10 sessões de captura de pacote por região e assinatura. Esse limite se aplica somente a sessões de toohello e não se aplica a toohello salva arquivos de captura de pacote localmente no hello VM ou em uma conta de armazenamento.

> [!IMPORTANT]
> A captura de pacotes requer uma extensão da máquina virtual `AzureNetworkWatcherExtension`. Para instalar a extensão de saudação em uma VM do Windows, visite [extensão de máquina virtual do agente do Inspetor de rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para a visita de VM do Linux [extensão de máquina virtual do agente do Inspetor de rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).

informações de saudação tooreduce capturar informações de saudação tooonly desejado, Olá as opções a seguir está disponível para uma sessão de captura de pacote:

**Configuração da captura**

|Propriedade|Descrição|
|---|---|
|**Máximo de bytes por pacote (bytes)** | Olá o número de bytes de cada pacote que são capturadas, todos os bytes são capturados se deixado em branco. Olá o número de bytes de cada pacote que são capturadas, todos os bytes são capturados se deixado em branco. Se você precisar somente cabeçalho de IPv4 hello – indicar 34 aqui |
|**Máximo de bytes por sessão (bytes)** | Número total de bytes em que é capturado, quando o valor de saudação é atingido Olá término da sessão.|
|**Tempo limite (segundos)** | Define uma restrição de tempo no pacote de saudação capturar a sessão. valor padrão de saudação é 18000 segundos ou cinco horas.|

**Filtragem (opcional)**

|Propriedade|Descrição|
|---|---|
|**Protocolo** | Olá toofilter de protocolo para o pacote de saudação de captura. os valores disponíveis Olá são TCP, UDP e todos.|
|**Endereço IP local** | Esse valor filtra Olá toopackets de captura de pacote em que o endereço IP local Olá corresponde esse valor de filtro.|
|**Porta local** | Este pacote de saudação do valor filtros capturar toopackets onde porta local Olá corresponde a esse valor de filtro.|
|**Endereço IP remoto** | Este pacote de saudação do valor filtros capturar toopackets onde IP remoto Olá corresponde a esse valor de filtro.|
|**Porta remota** | Este pacote de saudação do valor filtros capturar toopackets onde porta remota Olá corresponde a esse valor de filtro.|

### <a name="next-steps"></a>Próximas etapas

Saiba como você pode gerenciar a captura de pacote por meio do portal Olá visitando [gerenciar captura de pacote no portal do Azure de saudação](network-watcher-packet-capture-manage-portal.md) ou com o PowerShell visitando [gerenciar de captura de pacote com o PowerShell](network-watcher-packet-capture-manage-powershell.md).

Saiba como o pacote pró-ativo toocreate captura com base em alertas de máquina virtual visitando [criar uma captura de pacote de disparo de alerta](network-watcher-alert-triggered-packet-capture.md)

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













