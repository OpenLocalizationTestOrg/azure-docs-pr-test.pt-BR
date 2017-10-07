---
title: "problemas comuns de aaaHow tootroubleshoot durante a criação do VHD | Microsoft Docs"
description: "Solução de problemas de toocommon respostas perguntas e problemas durante a criação do VHD."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: e4ff09a979bdf575badff2d33f2299abb17c947d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-common-issues-encountered-during-vhd-creation"></a>Como tootroubleshoot os problemas comuns encontrados durante a criação do VHD
Este artigo é fornecida toohelp um publicador do Azure Marketplace e/ou coadministrador que pode enfrentar um problema ou dúvidas comuns ao publicar ou gerenciar suas soluções de máquina virtual.

1. Como alterar o nome de saudação do host Olá?
   
    Depois que a VM é criada, os usuários não é possível atualizar o nome de saudação do host de saudação.
2. Como tooreset Olá serviços de área de trabalho remota ou sua senha de logon?
   
   * [Referência de VM do Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [Referência de VM do Linux](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. Como toogenerate novo ssh certificados?
   
   Consulte o link toohello: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
4. Como tooconfigure um certificado VPN aberto?
   
   Consulte o link toohello: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)
5. O que é a política de suporte de saudação para executar o software de servidor da Microsoft no ambiente de máquina virtual do Microsoft Azure hello (uma infraestrutura como serviço)?
   
   Consulte o link toohello: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)
6. As máquinas virtuais têm algum identificador exclusivo?
   
   O Azure codifica a ID exclusiva da VM do Azure em cada VM. Consulte detalhes neste blog e na documentação.
7. Em uma VM como gerenciar extensão do script personalizado Olá na tarefa de inicialização Olá?
   
   Consulte o link toohello: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)
8. Como toocreate uma VM do hello usando o portal do Azure Olá VHD carregado toopremium armazenamento?
   
   Ainda não oferecemos suporte a essa funcionalidade.
9. Um aplicativo de 32 bits com suporte no Azure Marketplace de Olá?
   
   Consulte toohello link para obter detalhes sobre a política de suporte de saudação: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)
10. Sempre que estou tentando toocreate uma imagem do meu VHDs, recebo o erro Olá ". VHD já está registrado com o repositório de imagem como recurso hello"no PowerShell. Eu não criei qualquer imagem antes, nem encontrei qualquer imagem com esse nome no Azure. Como resolver isso?
    
    Isso geralmente acontecer se o usuário Olá provisionado uma VM nesse VHD e não há um bloqueio em que o VHD. Verifique se não há uma VM alocada a partir desse VHD. Se o erro de saudação persistir, gere um tíquete de suporte usando este link ou de saudação publicação portal relativas a esta (detalhes são fornecidos na resposta de saudação de pergunta 11).
