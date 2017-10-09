---
title: Verifique se aaaIntroduction tooIP fluxo no Inspetor de rede do Azure | Microsoft Docs
description: "Esta página fornece uma visão geral de rede IP de Inspetor de hello fluxo Verifique a capacidade"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a>Fluxo de tooIP Introdução verificar em observador de rede do Azure

Fluxo IP verificar verifica se um pacote é permitido ou negado tooor de uma máquina virtual com base nas informações de 5 tuplas. Essas informações consistem em direção, protocolo, IP local, IP remoto, porta local e porta remota. Se o pacote de saudação é negado por um grupo de segurança, nome de saudação de regra Olá negado pacote de saudação é retornado. Enquanto qualquer IP de origem ou de destino pode ser escolhido, esse recurso ajuda os administradores a diagnosticar rapidamente toohello ou problemas de conectividade de internet e de ou toohello ambiente de local.

A verificação de fluxo de IP tem como alvo uma interface de rede de uma máquina virtual. Fluxo de tráfego é verificado com base em tooor de configurações de saudação configurada desta interface de rede. Esse recurso é útil para confirmar se uma regra em um grupo de segurança de rede está bloqueando tooor de tráfego de entrada ou de saída de uma máquina virtual.

Verifique se uma instância do observador de rede necessidades toobe criado em todas as regiões que você planeje toorun fluxo IP. Observador de rede é um serviço regional e só pode ser executado com base nos recursos em Olá mesma região. Isso não afeta a saudação resultados do fluxo IP de verificar como rota Olá associada Olá que NIC ainda será retornada.

![1][1]

## <a name="next-steps"></a>Próximas etapas

Visite Olá toolearn do artigo a seguir se um pacote é permitido ou negado para uma máquina virtual por meio do portal hello. [Verifique se o tráfego é permitido em uma VM com IP fluxo verificar usando o portal de saudação](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












