---
title: Baixar um VHD do Windows do Azure | Microsoft Docs
description: Baixe um VHD do Windows usando o portal do Azure.
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
ms.openlocfilehash: d8bf89a4b7c2a158302f9ba09a182a3d8d062adc
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2017
---
# <a name="download-a-windows-vhd-from-azure"></a>Baixar um VHD do Windows Azure

Neste artigo, você aprenderá a baixar um arquivo [VHD (disco rígido virtual do Windows)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) do Azure usando o portal do Azure. 

As VMs (máquinas virtuais) do Azure usam [discos](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) como locais para armazenar um sistema operacional, aplicativos e dados. Todas as VMs do Azure têm, pelo menos, dois discos – um disco do sistema operacional Windows e um disco temporário. O disco do sistema operacional é inicialmente criado com base em uma imagem, e tanto o disco do sistema operacional quanto a imagem são VHDs armazenados em uma conta de armazenamento do Azure. Máquinas virtuais também podem ter um ou mais discos de dados que também são armazenados em VHDs.

## <a name="stop-the-vm"></a>Pare a VM.

Não é possível baixar um VHD por meio do Azure se ele estiver anexado a uma VM em execução. Você precisa parar a VM para baixar um VHD. Se você quiser usar um VHD como uma [imagem](tutorial-custom-images.md) para criar outras VMs com novos discos, use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) para generalizar o sistema operacional contido no arquivo e interromper a VM. Para usar o VHD como um disco de uma nova instância de uma VM existente ou um disco de dados, basta parar e desalocar a VM.

Para usar o VHD como uma imagem para criar outras VMs, conclua estas etapas:

1.  Se ainda não tiver feito isso, entre no [portal do Azure](https://portal.azure.com/).
2.  [Conectar-se à VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
3.  Na VM, abra uma janela de prompt de comando como administrador.
4.  Altere o diretório para *%windir%\system32\sysprep* e execute sysprep.exe.
5.  Na caixa de diálogo Ferramenta de Preparação do Sistema, selecione **Entrar na Configuração Inicial pelo Usuário do Sistema (OOBE)** e verifique se a opção **Generalizar** está marcada.
6.  Em Opções de Desligamento, selecione **Desligar** e **OK**. 

Para usar o VHD como um disco de uma nova instância de uma VM existente ou um disco de dados, conclua estas etapas:

1.  No menu Hub no portal do Azure, clique em **Máquinas Virtuais**.
2.  Selecione a VM na lista.
3.  Na folha da VM, clique em **Parar**.

    ![Parar a VM](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Gerar a URL de SAS

Para baixar o arquivo VHD, você precisa gerar uma URL de [SAS (assinatura de acesso compartilhado)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Quando a URL é gerada, uma hora de expiração é atribuída à URL.

1.  No menu da folha da VM, clique em **Discos**.
2.  Selecione o disco do sistema operacional da VM e clique em **Exportar**.
3.  Defina o tempo de expiração da URL como *36000*.
4.  Clique em **Gerar URL**.

    ![Gerar a URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> O tempo de expiração é aumentado de padrão a fim de fornecer tempo suficiente para baixar o arquivo VHD grande para um sistema operacional Windows Server. Você pode esperar que um arquivo VHD que contém o sistema operacional Windows Server leve várias horas para ser baixado, dependendo da conexão. Se você estiver baixando um VHD para um disco de dados, a hora padrão será suficiente. 
> 
> 

## <a name="download-vhd"></a>Baixar o VHD

1.  Na URL que foi gerada, clique em Baixar o arquivo VHD.

    ![Baixar o VHD](./media/download-vhd/export-download.png)

2.  Talvez você precise clicar em **Salvar** no navegador para iniciar o download. O nome padrão do arquivo VHD é *abcd*.

    ![Clicar em Salvar no navegador](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Próximas etapas

- Saiba como [carregar um arquivo VHD no Azure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
- [Criar discos gerenciados de discos não gerenciados em uma conta de armazenamento](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
- [Gerenciar discos do Azure com o PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

