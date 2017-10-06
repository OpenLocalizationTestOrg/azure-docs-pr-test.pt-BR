---
title: aaaSecure aplicativos e recursos no Azure RemoteApp | Microsoft Docs
description: Saiba como toolock para baixo de aplicativos e recursos no Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7fbade87-a453-426d-bfa5-c72227ea83cd
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 26325826e92855a12a0087f19a3e32cbe1116449
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a>Proteger aplicativos e recursos no Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

O Azure RemoteApp fornece aos usuários acesso gerenciado toocentrally aplicativos da Windows que lhe permite controlar o que os usuários podem e não podem fazer.  Isso é particularmente útil quando o usuário hello está conectando a partir de um dispositivo não gerenciado (como seu Macbook pessoal) e você desejar toocontrol Olá usuário acesso ou a experiência.

Por exemplo, se você estiver usando o Active Directory para autenticação de usuário e queira tooprevent que os usuários copiem dados fora de um aplicativo, você pode configurar um usuário de tooblock de política de grupo de área de trabalho remota da cópia de dados.

Outro exemplo é se você quiser tooblock acesso à internet para um determinado aplicativo em sua coleção. Você pode criar uma regra de Firewall do Windows que bloqueia Olá acesso ao criar imagem Olá para sua coleção.

## <a name="implementation-options"></a>Opções de implementação
  Aqui estão as opções de implementação fundamentais hello, que podem ser usadas individualmente ou em tandem, conforme necessário:

1. Se sua coleção do RemoteApp está ingressado no domínio podem impor qualquer [política de grupo](https://technet.microsoft.com/library/cc725828.aspx) (com exceção de Olá Olá ocioso e desconectar tempo limite de políticas de descrito [aqui](../azure-subscription-service-limits.md)).
2. Como uma alternativa tooGroup política (se a coleção não está ingressado no domínio ou você não tem privilégios de saudação à direita no AD), você pode configurar [políticas locais](https://technet.microsoft.com/library/cc775702.aspx) em sua imagem de modelo.  Observe que essas políticas de grupos superam as políticas locais quando há um conflito.
3. Algumas configurações do sistema operacional/aplicativo não são configuráveis por meio da política, mas pode ser por meio da chave de registro usando Olá [RegEdit ferramenta](remoteapp-hybridtrouble.md) durante a configuração de sua imagem de modelo.
4. Você pode usar [Firewall do Windows](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) toocontrol tooand de acesso de rede da máquina Olá onde o aplicativo hello está sendo executado. Verifique se que você não bloquear Olá URLs e portas definidas aqui.
5. Você pode usar [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) toocontrol que os usuários de aplicativos e arquivos podem executar. Por exemplo, usuários experientes podem descobrir como toorun aplicativos que você não publicou, mas que estão disponíveis no hello imagem usada toocreate Olá coleção - o AppLocker pode bloquear isso.

## <a name="detailed-information"></a>Informações detalhadas
* Olá, as seguintes diretivas RDS é provavelmente toobe mais úteis:
  * [Redirecionamento de dispositivo e recurso](https://technet.microsoft.com/library/ee791794.aspx)
  * [Redirecionamento de impressora](https://technet.microsoft.com/library/ee791784.aspx)
  * [Perfis](https://technet.microsoft.com/library/ee791865.aspx).
* Observe que redirecionamentos Configurando via Olá módulo PowerShell do RemoteApp (como visto [aqui](remoteapp-redirection.md)) depende de política do hello cliente máquina tooenforce Olá, portanto, se a segurança é o principal objetivo do hello será tooenforce política de saudação por meio de Olá diretiva local de imagem de modelo ou por meio da política de grupo.
* [Políticas do Windows Server 2012 R2](https://technet.microsoft.com/library/hh831791.aspx).
* [Office 2013 políticas](https://technet.microsoft.com/library/cc178969.aspx) (incluindo [como toocustomize Olá barra de ferramentas Office](https://technet.microsoft.com/library/cc179143.aspx)).

