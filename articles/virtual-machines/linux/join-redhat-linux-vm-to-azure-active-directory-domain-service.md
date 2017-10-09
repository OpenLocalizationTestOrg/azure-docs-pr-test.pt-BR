---
title: aaaJoin tooan uma VM do Linux RedHat Azure Active Directory DS | Microsoft Docs
description: "Como toojoin uma tooan de RedHat Enterprise Linux 7 VM existente do Azure serviço de domínio Active Directory."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a><span data-ttu-id="be936-103">Unir um tooan RedHat Linux VM Azure serviço de domínio Active Directory</span><span class="sxs-lookup"><span data-stu-id="be936-103">Join a RedHat Linux VM tooan Azure Active Directory Domain Service</span></span>

<span data-ttu-id="be936-104">Este artigo mostra como toojoin uma tooan de máquina virtual do Red Hat Enterprise Linux (RHEL) 7 serviços de domínio do Active Directory (AADDS) do Azure gerenciados domínio.</span><span class="sxs-lookup"><span data-stu-id="be936-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="be936-105">requisitos de saudação são:</span><span class="sxs-lookup"><span data-stu-id="be936-105">hello requirements are:</span></span>

- [<span data-ttu-id="be936-106">uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="be936-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)

- [<span data-ttu-id="be936-107">arquivos de chave SSH pública e privada</span><span class="sxs-lookup"><span data-stu-id="be936-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

- [<span data-ttu-id="be936-108">Um controlador de domínio do Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="be936-108">an Azure Active Directory Domain Services DC</span></span>](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="be936-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="be936-109">Quick Commands</span></span>

<span data-ttu-id="be936-110">_Substitua quaisquer exemplos por suas próprias configurações._</span><span class="sxs-lookup"><span data-stu-id="be936-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a><span data-ttu-id="be936-111">Modo de implantação de tooclassic do comutador hello cli do azure</span><span class="sxs-lookup"><span data-stu-id="be936-111">Switch hello azure-cli tooclassic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="be936-112">Pesquise uma versão do RHEL e uma imagem</span><span class="sxs-lookup"><span data-stu-id="be936-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="be936-113">Criar uma VM Red Hat do Linux</span><span class="sxs-lookup"><span data-stu-id="be936-113">Create a Redhat Linux VM</span></span>

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-toohello-vm"></a><span data-ttu-id="be936-114">SSH toohello VM</span><span class="sxs-lookup"><span data-stu-id="be936-114">SSH toohello VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="be936-115">Atualizar os pacotes YUM</span><span class="sxs-lookup"><span data-stu-id="be936-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="be936-116">Instalar os pacotes necessários</span><span class="sxs-lookup"><span data-stu-id="be936-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="be936-117">Agora que pacotes Olá necessários estão instalados na máquina de virtual do Linux hello, Olá próxima tarefa é domínio gerenciado do toohello toojoin Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="be936-117">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

### <a name="discover-hello-aad-domain-services-managed-domain"></a><span data-ttu-id="be936-118">Descobrir o domínio gerenciado do serviços de domínio do AAD Olá</span><span class="sxs-lookup"><span data-stu-id="be936-118">Discover hello AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="be936-119">Inicializar o Kerberos</span><span class="sxs-lookup"><span data-stu-id="be936-119">Initialize kerberos</span></span>

<span data-ttu-id="be936-120">Certifique-se de que você especifique um usuário que pertence a toohello ' AAD controlador de domínio do grupo 'Administradores.</span><span class="sxs-lookup"><span data-stu-id="be936-120">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="be936-121">Apenas esses usuários podem ingressar em domínio gerenciado toohello dos computadores.</span><span class="sxs-lookup"><span data-stu-id="be936-121">Only these users can join computers toohello managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a><span data-ttu-id="be936-122">Ingressar Olá máquina toohello domínio</span><span class="sxs-lookup"><span data-stu-id="be936-122">Join hello machine toohello domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a><span data-ttu-id="be936-123">Verifique se machine Olá é toohello ingressado no domínio</span><span class="sxs-lookup"><span data-stu-id="be936-123">Verify hello machine is joined toohello domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="be936-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="be936-124">Next Steps</span></span>

* [<span data-ttu-id="be936-125">RHUI (Infraestrutura de Atualização do Red Hat) para as VMs Red Hat Enterprise do Linux sob demanda no Azure</span><span class="sxs-lookup"><span data-stu-id="be936-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="be936-126">Configurar o Cofre de Chaves para máquinas virtuais no Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="be936-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="be936-127">Implantar e gerenciar máquinas virtuais usando modelos do Gerenciador de recursos do Azure e hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="be936-127">Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI</span></span>](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
