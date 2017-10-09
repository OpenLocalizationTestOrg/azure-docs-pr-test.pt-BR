---
title: aaaUsing Outlook no Azure RemoteApp | Microsoft Docs
description: Saiba como tooconfigure e usar o Outlook no Azure RemoteApp | Microsoft Azure
services: remoteapp
documentationcenter: 
author: pavithir
manager: mbaldwin
ms.assetid: cb2a498f-9539-4522-a874-542114926a61
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 119d2629ac47bd8d20d617985a9b488068aa959f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-microsoft-outlook-in-azure-remoteapp"></a>Usando o Microsoft Outlook no Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

O Azure RemoteApp dá suporte ao Microsoft Outlook O365. Saiba mais sobre como o [Office funciona no Azure RemoteApp](remoteapp-officesubscription.md). Há algumas configurações recomendadas para o Outlook quando usado no Azure RemoteApp.

## <a name="cached-mode"></a>Modo cache
O modo cache é uma configuração recomendada para o uso do Outlook no Azure RemoteApp. Quando você configura um toouse de conta do Outlook 2013 modo em cache do Exchange, Outlook 2013 funciona de uma cópia local da caixa de correio do Microsoft Exchange do usuário de saudação que é armazenado em um arquivo de dados offline (arquivo OST) no computador do usuário hello, junto com hello catálogo de Endereços Offline (OAB). caixa de correio em cache Hello e OAB são atualizados periodicamente da saudação serviço O365. Leia mais sobre [Olá diferenças entre o modo em cache e online](https://technet.microsoft.com/library/jj683103.aspx).

Olá usuário pode selecionar **modo cache do Exchange** ou **modo Online** durante a instalação de conta ou alterando as configurações de conta de saudação. Você também pode implantar um modo ou outros hello usando Olá, ferramenta de personalização do Office (out) ou a diretiva de grupo.  

Leia [instruções passo a passo sobre como habilitar o modo cache](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc).

## <a name="search"></a>Pesquisar
No Azure RemoteApp, há limitações para o uso da pesquisa no Outlook. O Azure RemoteApp usa sessões de usuário de tooaccommodate de máquinas virtuais em pool. Indexação de pesquisa depende da ID da máquina hello, que é diferente para diferentes VMs. É possível que, toda vez que um usuário fizer logon no Azure RemoteApp, eles são tooa direcionado nova VM. Isso significaria, se habilitar a pesquisa local, indexador Olá será executado sempre que o ID da máquina Olá muda (quando o usuário hello está em uma máquina virtual diferente). Dependendo do tamanho de saudação do hello. Arquivo OST, indexador Olá poderia levar um longo tempo toocomplete e usar os recursos necessários para outros aplicativos. A pesquisa não seria apenas lenta, como talvez não produzisse resultados. Usar um perfil de conta do modo Online deve solucionar o problema, mas o desempenho geral, seria afetado devido a falta de toohello de um cache local (consulte Olá link acima para obter mais informações sobre a diferença Olá entre os modos online e em cache). Infelizmente, a pesquisa indexada/local não pode ser desabilitada e a pesquisa online não pode ser habilitada por padrão no Outlook 2013.

