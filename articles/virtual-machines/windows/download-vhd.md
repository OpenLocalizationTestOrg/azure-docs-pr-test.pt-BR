---
title: aaaDownload um VHD do Windows do Azure | Microsoft Docs
description: "Baixe um VHD do Windows usando Olá portal do Azure."
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
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a>Baixar um VHD do Windows Azure

Neste artigo, você aprenderá como toodownload uma [disco rígido virtual do Windows (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Olá de arquivo do Azure usando portal do Azure. 

Máquinas virtuais (VMs) em uso do Azure [discos](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) como toostore um local de um sistema operacional, aplicativos e dados. Todas as VMs do Azure têm, pelo menos, dois discos – um disco do sistema operacional Windows e um disco temporário. disco do sistema operacional Olá é inicialmente criado de uma imagem e disco do sistema operacional hello e imagem Olá são VHDs armazenados em uma conta de armazenamento do Azure. Máquinas virtuais também podem ter um ou mais discos de dados que também são armazenados em VHDs.

## <a name="stop-hello-vm"></a>Parar Olá VM

Não é possível baixar um VHD do Azure, se ele estiver anexado tooa executando VM. É necessário toodownload VM da saudação toostop um VHD. Se você quiser toouse um VHD como um [imagem](tutorial-custom-images.md) toocreate outras VMs com novos discos, use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize Olá sistema operacional contido no arquivo hello e, em seguida, parar Olá VM. Olá toouse VHD como um disco para uma nova instância de uma VM existente ou um disco de dados, você só precisa toostop e desalocar Olá VM.

toouse Olá VHD como uma imagem toocreate outras VMs, conclua estas etapas:

1.  Se você ainda não fez isso, entre no toohello [portal do Azure](https://portal.azure.com/).
2.  [Conecte-se a VM de toohello](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
3.  No hello VM, abra a janela de Prompt de comando hello como um administrador.
4.  Altere o diretório de saudação muito*%windir%\system32\sysprep* e execute sysprep.exe.
5.  Na caixa de diálogo Ferramenta de preparação do sistema hello, selecione **Enter System Out-of-Box Experience (OOBE)**e certifique-se de que **generalizar** está selecionado.
6.  Em Opções de Desligamento, selecione **Desligar** e **OK**. 

Olá toouse VHD como um disco para uma nova instância de uma VM existente ou um disco de dados, execute estas etapas:

1.  No menu de Hub de saudação do hello portal do Azure, clique em **máquinas virtuais**.
2.  Selecione Olá VM na lista de saudação.
3.  Na folha de saudação para Olá VM, clique em **parar**.

    ![Parar a VM](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Gerar a URL de SAS

arquivo VHD Olá toodownload, você precisa toogenerate um [assinatura de acesso compartilhado (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL. Quando Olá URL é gerado, um tempo de expiração é atribuído toohello URL.

1.  No menu de saudação da folha de saudação para Olá VM, clique em **discos**.
2.  Selecione o disco do sistema operacional Olá para Olá VM e, em seguida, clique em **exportar**.
3.  Definir o tempo de expiração de saudação da saudação URL muito*36000*.
4.  Clique em **Gerar URL**.

    ![Gerar a URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> tempo de expiração de saudação é aumentado de saudação padrão tooprovide tempo suficiente toodownload Olá arquivo VHD grande para um sistema operacional Windows Server. Você pode esperar um arquivo VHD que contém tootake de sistema operacional Windows Server Olá toodownload de várias horas dependendo de sua conexão. Se você estiver baixando um VHD para um disco de dados, o tempo padrão de saudação é suficiente. 
> 
> 

## <a name="download-vhd"></a>Baixar o VHD

1.  Olá URL que foi gerado, clique em arquivo VHD de saudação do Download.

    ![Baixar o VHD](./media/download-vhd/export-download.png)

2.  Talvez seja necessário tooclick **salvar** no download de Olá Olá navegador toostart. saudação padrão nome para o arquivo VHD Olá é *abcd*.

    ![Clique em Salvar no navegador Olá](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Próximas etapas

- Saiba como muito[carregar um tooAzure do arquivo VHD](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
- [Criar discos gerenciados de discos não gerenciados em uma conta de armazenamento](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
- [Gerenciar discos do Azure com o PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

