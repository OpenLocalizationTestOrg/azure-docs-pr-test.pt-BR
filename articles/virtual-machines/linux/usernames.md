---
title: "aaaSelecting nomes de usuário para Linux | Microsoft Docs"
description: "Saiba como nomes de usuário tooselect para uma máquina virtual do Linux no Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a>Selecionando nomes de usuário para Linux no Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Quando você provisionar uma máquina virtual do Linux no Azure, você deve especificar nome de saudação de um usuário não raiz que você pode usar mais tarde toolog em Olá VM. Você pode escolher nome de saudação do novo usuário do hello, ou se provisionamento via Olá portal clássico do Azure você pode aceitar o padrão de saudação nome "azureuser".

Na maioria dos casos, esse usuário não existe na imagem base hello e será criado durante o processo de provisionamento de saudação. Se o usuário Olá existir na imagem de VM base hello, agente do Linux Azure Olá simplesmente configura senha hello e/ou uma chave SSH para que o usuário com base nas informações de saudação que você especificou ao criar hello VM.

**Entretanto**, o Linux define um conjunto de nomes de usuário que não deve ser usado ao criar novos usuários. Olá provisionamento processo será **falha** se você tentar tooprovision uma VM do Linux usando um usuário existente do sistema, que é definido como um usuário com UID 0-99. Um exemplo típico é hello `root` usuário, que tem o UID 0.

* Consulte também: [Base padrão do Linux - Intervalos de ID de usuário](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)

a seguir Olá é uma lista de usuários comuns do sistema internas para CentOS e Ubuntu que você deve evitar usar ao provisionar uma máquina virtual do Linux no Azure. Essa lista é apenas um exemplo, consulte toohello documentação para sua distribuição tooensure esse nome de usuário Olá que você escolher não está em conflito com um usuário de sistema existente.

## <a name="centos"></a>CentOS
* abrt
* adm
* audio
* bin
* cdrom
* cgred
* daemon
* dbus
* dialout
* dip
* disk
* floppy
* ftp
* ftp
* games
* gopher
* haldaemon
* halt
* kmem
* lock
* lp
* mail
* man
* mem
* nfsnobody
* nobody
* ntp
* operator
* oprofile
* postdrop
* postfix
* qpidd
* root
* rpc
* rpcuser
* saslauth
* shutdown
* slocate
* sshd
* stapdev
* stapusr
* sync
* sys
* tape
* test
* tcpdump
* tty
* users
* utempter
* utmp
* uucp
* vcsa
* video
* wheel

## <a name="ubuntu"></a>Ubuntu
* adm
* admin
* audio
* backup
* bin
* cdrom
* crontab
* daemon
* dialout
* dip
* disk
* fax
* floppy
* fuse
* games
* gnats
* irc
* kmem
* landscape
* libuuid
* list
* lp
* mail
* man
* messagebus
* mlocate
* netdev
* news
* nobody
* nogroup
* operator
* plugdev
* proxy
* root
* sasl
* shadow
* src
* ssh
* sshd
* staff
* sudo
* sync
* sys
* syslog
* tape
* tty
* users
* utmp
* uucp
* video
* voice
* whoopsie
* www-data

