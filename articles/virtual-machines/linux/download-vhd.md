---
title: aaaDownload um VHD do Linux do Azure | Microsoft Docs
description: "Baixar um VHD do Linux usando Olá CLI do Azure e Olá portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a>Baixar um VHD do Linux por meio do Azure

Neste artigo, você aprenderá como toodownload uma [Linux virtual VHD (disco rígido)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Olá arquivo do Azure usando a CLI do Azure e o portal do Azure. 

Máquinas virtuais (VMs) em uso do Azure [discos](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) como toostore um local de um sistema operacional, aplicativos e dados. Todas as VMs do Azure têm, pelo menos, dois discos – um disco do sistema operacional Windows e um disco temporário. disco do sistema operacional Olá é inicialmente criado de uma imagem e disco do sistema operacional hello e imagem Olá são VHDs armazenados em uma conta de armazenamento do Azure. Máquinas virtuais também podem ter um ou mais discos de dados que também são armazenados em VHDs.

Se você ainda não fez isso, instale a [CLI 2.0 do Azure](https://docs.microsoft.com/cli/azure/install-az-cli2).

## <a name="stop-hello-vm"></a>Parar Olá VM

Não é possível baixar um VHD do Azure, se ele estiver anexado tooa executando VM. É necessário toodownload VM da saudação toostop um VHD. Se você quiser toouse um VHD como um [imagem](tutorial-custom-images.md) toocreate outras VMs com novos discos, você precisa toodeprovision e generalizar sistema de operacional Olá contido em Olá de arquivo e parar Olá VM. Olá toouse VHD como um disco para uma nova instância de uma VM existente ou um disco de dados, você só precisa toostop e desalocar Olá VM.

toouse Olá VHD como uma imagem toocreate outras VMs, conclua estas etapas:

1. Use SSH, nome da conta hello e endereço IP público de saudação do hello VM tooconnect tooit e seu provisionamento. Olá + usuário parâmetro também remove a última conta de usuário provisionado hello. Se você é trazer credenciais de conta no toohello VM, deixe este + parâmetro de usuário. Olá, exemplo a seguir remove última conta de usuário provisionado hello:

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. Entrar tooyour conta do Azure com [logon az](https://docs.microsoft.com/cli/azure/#login).
3. Parar e desalocar Olá VM.

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. Generalize Olá VM. 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

Olá toouse VHD como um disco para uma nova instância de uma VM existente ou um disco de dados, execute estas etapas:

1.  Entrar toohello [portal do Azure](https://portal.azure.com/).
2.  No menu de Hub hello, clique em **máquinas virtuais**.
3.  Selecione Olá VM na lista de saudação.
4.  Na folha de saudação para Olá VM, clique em **parar**.

    ![Parar a VM](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Gerar a URL de SAS

arquivo VHD Olá toodownload, você precisa toogenerate um [assinatura de acesso compartilhado (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL. Quando Olá URL é gerado, um tempo de expiração é atribuído toohello URL.

1.  No menu de saudação da folha de saudação para Olá VM, clique em **discos**.
2.  Selecione o disco do sistema operacional Olá para Olá VM e, em seguida, clique em **exportar**.
3.  Clique em **Gerar URL**.

    ![Gerar a URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a>Baixar o VHD

1.  Olá URL que foi gerado, clique em arquivo VHD de saudação do Download.

    ![Baixar o VHD](./media/download-vhd/export-download.png)

2.  Talvez seja necessário tooclick **salvar** no download de Olá Olá navegador toostart. saudação padrão nome para o arquivo VHD Olá é *abcd*.

    ![Clique em Salvar no navegador Olá](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Próximas etapas

- Saiba como muito[carregar e criar uma VM do Linux do disco personalizado com hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
- [Gerenciar discos do Azure Olá CLI do Azure](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

