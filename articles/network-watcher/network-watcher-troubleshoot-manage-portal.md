---
title: "aaaTroubleshoot conexões - PowerShell e o Gateway de rede Virtual do Azure | Microsoft Docs"
description: "Esta página explica como toouse Olá observador de rede do Azure solucionar problemas do cmdlet do PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>Como solucionar problemas de conexões e gateway de rede virtual do usando o PowerShell do Observador de rede do Azure

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API REST](network-watcher-troubleshoot-manage-rest.md)

Observador de rede fornece vários recursos que diz respeito a toounderstanding seus recursos de rede no Azure. Um desses recursos é a solução de problemas de recursos. Recursos de solução de problemas pode ser chamada por meio do portal de saudação, o PowerShell, CLI ou API REST. Quando chamado, o observador de rede inspeciona a integridade de saudação de um Gateway de rede Virtual ou uma Conexão e retorna suas descobertas.

## <a name="before-you-begin"></a>Antes de começar

Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.

Para obter uma lista de tipos de gateway com suporte, visite [Tipos de Gateway com suporte](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Visão geral

Solução de problemas de recursos fornece a capacidade de saudação solucionar problemas que surgem com Gateways de rede Virtual e conexões. Quando é feita uma solicitação tooresource de solução de problemas, os logs estão sendo consultados e inspecionado. Quando inspeção estiver concluída, os resultados de saudação são retornados. Solicitações de recursos para solução de problemas de solicitações são de longa execução, que pode levar vários tooreturn de minutos que um resultado. logs de saudação de solução de problemas são armazenados em um contêiner em uma conta de armazenamento especificado.

## <a name="troubleshoot-a-gateway-or-connection"></a>Solucionar problemas de um gateway ou conexão

1. Navegue toohello [portal do Azure](https://portal.azure.com) e clique em **rede** > **observador de rede** > **diagnóstico de VPN**
2. Selecione uma **Assinatura**, **Grupo de Recursos** e **Local**.
3. Solução de problemas de recurso retorna dados sobre a integridade de saudação do recurso de saudação. Ele também salva a conta de armazenamento tooa logs relevantes toobe revisado. Clique em **conta de armazenamento** tooselect uma conta de armazenamento.
4. Em Olá **contas de armazenamento** folha, selecione uma conta de armazenamento existente ou clique em **+ conta de armazenamento** toocreate um novo.
5. Em Olá **contêineres** folha, escolha um contêiner existente ou clique em **+ contêiner** toocreate um novo contêiner. Quando concluído, clique em **Selecionar**
6. Selecione Olá tootroubleshoot de recursos de Gateway e de Conexão e clique em **Iniciar de solução de problemas**

Se vários recursos forem selecionados, a solução de problemas será executada simultaneamente em recursos de gateway. Não pode ser executada em uma conexão e o gateway em Olá associado simultaneamente. É recomendável tootroubleshoot gateways primeiro a solução de problemas de conexão é um processo mais longo. Enquanto o diagnóstico de VPN está em execução em uma saudação do recurso **TROUBLESHOOTING STATUS** coluna mostrará um status de **em execução**

Ao concluir, Olá alterações de coluna de status muito**Íntegro** ou **Unhealthy**.

![Solução de problemas concluída][2]

## <a name="understanding-hello-results"></a>Entendendo os resultados da saudação

Em Olá **detalhes** seção da janela de Olá Olá **Status** guia mostra o status de saudação de solução de problemas de última Olá execução no recurso de saudação selecionado. Resultados do diagnóstico mais recente Olá são mostrados xx minutos após o hello executado pela última vez.

|Propriedade  |Descrição  |
|---------|---------|
|Recurso     | Um recurso de toohello de link.        |
|Caminho de armazenamento     |  Conta de armazenamento do caminho toohello e contêiner que contêm logs hello (se qualquer produzidas durante a saudação executar). Essa configuração não persiste após sair do portal de saudação.        |
|Resumo     | Resumo de integridade de recursos de saudação.        |
|Detalhes     | Informações detalhadas sobre a integridade de recurso hello.        |
|Última execução     | Olá Olá tempo última solução de problemas de tempo foi executado.        |


Olá **ação** guia fornece diretrizes gerais sobre como tooresolve Olá problema. Se uma ação pode ser executada para o problema de saudação, um link é fornecido com diretrizes adicionais. No caso de Olá onde não há nenhuma orientação adicional, resposta Olá fornece Olá url tooopen um caso de suporte.  Para obter mais informações sobre propriedades de saudação de resposta hello e o que está incluído, visite [visão geral da solução de problemas do Inspetor de rede](network-watcher-troubleshoot-overview.md)


## <a name="next-steps"></a>Próximas etapas

Se as configurações foram alteradas se parar a conectividade de VPN, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack para baixo Olá rede segurança e o grupo de regras de segurança que podem ser em questão.


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
