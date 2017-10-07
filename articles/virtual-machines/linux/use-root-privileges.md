---
title: "privilégios de raiz aaaUse em máquinas virtuais do Linux | Microsoft Docs"
description: "Saiba como raiz toouse privilégios em uma máquina virtual do Linux no Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a>Utilizando privilégios de raiz nas máquinas virtuais Linux do Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Por padrão, Olá `root` usuário está desabilitado em máquinas virtuais Linux no Azure. Os usuários podem executar comandos com privilégios elevados usando Olá `sudo` comando. No entanto, experiência Olá pode variar dependendo de como o sistema Olá foi provisionado.

1. **Chave SSH e senha ou senha apenas** -Olá VM foi provisionado com um certificado (`.CER` arquivo) ou chave SSH, bem como uma senha, ou apenas um nome de usuário e senha. Nesse caso `sudo` solicitará a senha do usuário Olá antes de executar o comando de saudação.
2. **Somente a chave SSH** -Olá VM foi provisionado com um certificado (`.cer`, `.pem`, ou `.pub` arquivo) ou a chave SSH, mas nenhuma senha.  Nesse caso `sudo` **não** solicitar a senha do usuário Olá antes de executar o comando hello.

## <a name="ssh-key-and-password-or-password-only"></a>SSH chave e a senha ou a senha apenas
Faça logon na máquina virtual do Linux hello usando a autenticação de senha ou chave SSH, execute os comandos usando `sudo`, por exemplo:

    # sudo <command>
    [sudo] password for azureuser:

Nesse caso Olá usuário será solicitado para uma senha. Depois de inserir a senha Olá `sudo` executará o comando Olá com `root` privilégios.

Você também pode habilitar sudo passwordless editando Olá `/etc/sudoers.d/waagent` arquivo, por exemplo:

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

Essa alteração permitirá sudo passwordless por usuário hello "azureuser".

## <a name="ssh-key-only"></a>SSH chave somente
Faça logon na máquina virtual do Linux hello usando autenticação de chave SSH, execute os comandos usando `sudo`, por exemplo:

    # sudo <command>

Nesse caso o usuário Olá será **não** ser solicitada uma senha. Após pressionar `<enter>`, `sudo` executará o comando Olá com `root` privilégios.

