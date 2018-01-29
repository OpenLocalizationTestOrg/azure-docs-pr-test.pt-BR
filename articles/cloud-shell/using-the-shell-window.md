---
title: Usando a janela do Azure Cloud Shell | Microsoft Docs
description: "Visão geral de como usar a janela do Azure Cloud Shell."
services: azure
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/16/2017
ms.author: juluk
ms.openlocfilehash: 4eb5680c618d78e0722e1eb4a0f551f26b4dc902
ms.sourcegitcommit: cf42a5fc01e19c46d24b3206c09ba3b01348966f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/29/2017
---
# <a name="using-the-azure-cloud-shell-window"></a>Usando a janela do Azure Cloud Shell

Este documento explica como usar a janela do Cloud Shell.

## <a name="swap-between-bash-and-powershell-environments"></a>Alternar entre os ambientes Bash e PowerShell
![](media/using-the-shell-window/env-selector.png)

Use o seletor de ambiente na barra de ferramentas do Cloud Shell para alternar entre os ambientes Bash e PowerShell.

## <a name="restart-cloud-shell"></a>Reiniciar o Cloud Shell
![](media/using-the-shell-window/restart.png)
> [!WARNING]
> Reiniciar o Cloud Shell redefinirá o estado do computador, e quaisquer arquivos não persistentes no seu compartilhamento de arquivos do Azure serão perdidos.

* Clique no ícone de reinicialização na barra de ferramentas do Cloud Shell para redefinir o estado da máquina.

## <a name="minimize--maximize-cloud-shell-window"></a>Minimizar e maximizar a janela do Cloud Shell
![](media/using-the-shell-window/minmax.png)
* Clique no ícone de minimizar no canto superior direito da janela para ocultá-lo. Clique novamente no ícone do Cloud Shell para reexibir.
* Clique no ícone de maximizar para definir a janela com a altura máxima. Para restaurar a janela ao tamanho anterior, clique em Restaurar.

## <a name="concurrent-sessions"></a>Sessões simultâneas
O Cloud Shell permite várias sessões simultâneas em guias do navegador permitindo que cada sessão exista como um processo do Bash separado.
Ao sair de uma sessão, saia de cada janela de sessão, pois cada processo é executado de forma independente apesar de serem executados no mesmo computador.

## <a name="copy-and-paste"></a>Copiar e colar
[!include [copy-paste](../../includes/cloud-shell-copy-paste.md)]

## <a name="resize-cloud-shell-window"></a>Redimensionar a janela do Cloud Shell
* Clique e arraste a borda superior da barra de ferramentas para cima ou para baixo para redimensionar a janela do Cloud Shell.

## <a name="scrolling-text-display"></a>Rolagem pela exibição de texto
* Role com o mouse ou teclado para ir ao texto de terminal.

## <a name="changing-the-text-size"></a>Alterar o tamanho do texto
![](media/using-the-shell-window/text-size.png)
* Clique no ícone de configurações na parte superior esquerda da janela, em seguida, passe o mouse sobre a opção "Tamanho do texto" e selecione o tamanho do texto desejado. Sua seleção persistirá entre as sessões.

## <a name="exit-command"></a>Comando de saída
Executar `exit` encerra a sessão ativa. Esse comportamento ocorre por padrão após 20 minutos sem interação.

## <a name="next-steps"></a>Próximas etapas

[Guia de início rápido do Bash no Cloud Shell](quickstart.md)
[Guia de início rápido do PowerShell no Cloud Shell](quickstart-powershell.md)