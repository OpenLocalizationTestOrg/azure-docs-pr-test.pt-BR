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
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="0c66f-103">Utilizando privilégios de raiz nas máquinas virtuais Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="0c66f-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="0c66f-104">Por padrão, Olá `root` usuário está desabilitado em máquinas virtuais Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="0c66f-104">By default, hello `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="0c66f-105">Os usuários podem executar comandos com privilégios elevados usando Olá `sudo` comando.</span><span class="sxs-lookup"><span data-stu-id="0c66f-105">Users can run commands with elevated privileges by using hello `sudo` command.</span></span> <span data-ttu-id="0c66f-106">No entanto, experiência Olá pode variar dependendo de como o sistema Olá foi provisionado.</span><span class="sxs-lookup"><span data-stu-id="0c66f-106">However, hello experience may vary depending on how hello system was provisioned.</span></span>

1. <span data-ttu-id="0c66f-107">**Chave SSH e senha ou senha apenas** -Olá VM foi provisionado com um certificado (`.CER` arquivo) ou chave SSH, bem como uma senha, ou apenas um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="0c66f-107">**SSH key and password OR password only** - hello virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="0c66f-108">Nesse caso `sudo` solicitará a senha do usuário Olá antes de executar o comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c66f-108">In this case `sudo` will prompt for hello user's password before executing hello command.</span></span>
2. <span data-ttu-id="0c66f-109">**Somente a chave SSH** -Olá VM foi provisionado com um certificado (`.cer`, `.pem`, ou `.pub` arquivo) ou a chave SSH, mas nenhuma senha.</span><span class="sxs-lookup"><span data-stu-id="0c66f-109">**SSH key only** - hello virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="0c66f-110">Nesse caso `sudo` **não** solicitar a senha do usuário Olá antes de executar o comando hello.</span><span class="sxs-lookup"><span data-stu-id="0c66f-110">In this case `sudo` **will not** prompt for hello user's password before executing hello command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="0c66f-111">SSH chave e a senha ou a senha apenas</span><span class="sxs-lookup"><span data-stu-id="0c66f-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="0c66f-112">Faça logon na máquina virtual do Linux hello usando a autenticação de senha ou chave SSH, execute os comandos usando `sudo`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0c66f-112">Log into hello Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="0c66f-113">Nesse caso Olá usuário será solicitado para uma senha.</span><span class="sxs-lookup"><span data-stu-id="0c66f-113">In this case hello user will be prompted for a password.</span></span> <span data-ttu-id="0c66f-114">Depois de inserir a senha Olá `sudo` executará o comando Olá com `root` privilégios.</span><span class="sxs-lookup"><span data-stu-id="0c66f-114">After entering hello password `sudo` will run hello command with `root` privileges.</span></span>

<span data-ttu-id="0c66f-115">Você também pode habilitar sudo passwordless editando Olá `/etc/sudoers.d/waagent` arquivo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0c66f-115">You can also enable passwordless sudo by editing hello `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="0c66f-116">Essa alteração permitirá sudo passwordless por usuário hello "azureuser".</span><span class="sxs-lookup"><span data-stu-id="0c66f-116">This change will allow for passwordless sudo by hello user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="0c66f-117">SSH chave somente</span><span class="sxs-lookup"><span data-stu-id="0c66f-117">SSH Key Only</span></span>
<span data-ttu-id="0c66f-118">Faça logon na máquina virtual do Linux hello usando autenticação de chave SSH, execute os comandos usando `sudo`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0c66f-118">Log into hello Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="0c66f-119">Nesse caso o usuário Olá será **não** ser solicitada uma senha.</span><span class="sxs-lookup"><span data-stu-id="0c66f-119">In this case hello user will **not** be prompted for a password.</span></span> <span data-ttu-id="0c66f-120">Após pressionar `<enter>`, `sudo` executará o comando Olá com `root` privilégios.</span><span class="sxs-lookup"><span data-stu-id="0c66f-120">After pressing `<enter>`, `sudo` will run hello command with `root` privileges.</span></span>

