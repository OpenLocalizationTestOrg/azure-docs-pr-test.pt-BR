---
title: "Máquinas virtuais do Azure do Gerenciador de servidores de aaaAccessing | Microsoft Docs"
description: "Obter uma visão geral de como tooview criar e gerenciar máquinas virtuais (VMs) do Azure no Gerenciador de servidores no Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: f8326aed105a64ca558f766d712cc68701f82c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>Acessando máquinas virtuais do Azure por meio do Gerenciador de Servidores
Usando o Gerenciador de Servidores no Visual Studio, você pode exibir informações sobre as máquinas virtuais hospedadas pelo Azure.

## <a name="accessing-virtual-machines-in-server-explorer"></a>Acessando máquinas virtuais no Gerenciador de Servidores
Se tiver máquinas virtuais hospedadas pelo Azure, você pode acessá-las no Gerenciador de Servidores. Você deve primeiro entrar no tooview de assinatura do Azure tooyour seus serviços móveis. toosign, abra o menu de atalho de saudação para Olá nó do Azure no Gerenciador de servidores e escolha **conectar tooMicrosoft Azure**.

### <a name="tooget-information-about-your-virtual-machines"></a>tooget informações sobre as máquinas virtuais
1. No Gerenciador de servidores, escolha uma máquina virtual e escolha tooshow chave Olá F4 sua janela de propriedades.
   
    Olá a tabela a seguir mostra quais propriedades estão disponíveis, mas eles são todos somente leitura. toochange-las, use Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
   
   | Propriedade | Descrição |
   | --- | --- |
   | Nome DNS |URL de saudação com hello endereço de Internet da máquina virtual de saudação. |
   | Ambiente |Para uma máquina virtual, o valor dessa propriedade Olá é sempre produção. |
   | Nome |nome de saudação da máquina virtual de saudação. |
   | Tamanho |Olá tamanho da saudação máquina virtual, que reflete a quantidade de saudação de memória e espaço em disco disponível. Para obter mais informações, consulte Como configurar os tamanhos de uma máquina virtual. |
   | Status |Os valores incluem Inicial, Iniciado, Parando, Parado e Recuperando Status. Se recuperando Status aparecer, o status atual da saudação é desconhecido. valores de saudação para essa propriedade diferem dos valores hello são usados em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885). |
   | SubscriptionID |ID da assinatura Olá para sua conta do Azure. Você pode exibir essas informações no hello [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885) exibindo as propriedades de saudação para uma assinatura. |
2. Escolha um nó do ponto de extremidade e, em seguida, exibir hello **propriedades** janela.
3. Olá, tabela a seguir descreve as propriedades disponíveis Olá de pontos de extremidade, mas eles são somente leitura. tooadd ou editar pontos de extremidade de saudação para uma máquina virtual, use Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885). 
   
   | Propriedade | Descrição |
   | --- | --- |
   | Nome |Um identificador para o ponto de extremidade de saudação. |
   | Porta privada |porta de saudação para aplicativo de tooyour interno de acesso de rede. |
   | Protocolo |protocolo Olá Olá a camada de transporte para este ponto de extremidade usa, TCP ou UDP. |
   | Porta pública |porta de saudação que é usada para acesso público tooyour aplicativo. |

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre como usar funções do Azure no Visual Studio, consulte [usando a área de trabalho remota com funções do Azure](vs-azure-tools-remote-desktop-roles.md).

