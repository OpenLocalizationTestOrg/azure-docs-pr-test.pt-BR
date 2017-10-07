---
title: "Verifique Olá unidade d: de uma VM de um disco de dados | Microsoft Docs"
description: "Descreve como toochange letras das unidades para uma VM do Windows para que você pode usar a unidade d: de saudação como uma unidade de dados."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a>Use a unidade d: de saudação como uma unidade de dados em uma VM do Windows
Se seu aplicativo precisa toouse Olá dados toostore unidade, siga essas instruções toouse outra letra de unidade de disco temporário hello. Nunca use Olá disco temporário toostore os dados que você precisa tookeep.

Se você redimensionar ou **parar (desalocar)** uma máquina virtual, isso pode disparar o posicionamento de máquina virtual de saudação tooa hipervisor novo. Um evento de manutenção planejada ou não planejada também pode disparar esse posicionamento. Nesse cenário, o disco temporário Olá será toohello reatribuídos a primeira letra de unidade disponível. Se você tiver um aplicativo que requer especificamente d:. hello, você precisa toofollow essas etapas tootemporarily mover Olá pagefile.sys, anexar um novo disco de dados e atribuir-lhe Olá letra D e, em seguida, mover Olá pagefile.sys unidade temporária toohello de volta. Uma vez concluído, Azure não terão volta Olá d: se Olá VM move hipervisor diferentes tooa.

Para obter mais informações sobre como o Azure usa o disco temporário hello, consulte [Noções básicas sobre unidades temporárias de saudação em máquinas virtuais do Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="attach-hello-data-disk"></a>Anexar disco de dados Olá
Primeiro, você precisará tooattach Olá dados disco toohello VM. toodo este usando o portal de hello, consulte [como tooattach um dados gerenciados de disco no portal do Azure de saudação](attach-managed-disk-portal.md).

## <a name="temporarily-move-pagefilesys-tooc-drive"></a>Mover temporariamente pagefile.sys tooC unidade
1. Conecte-se a máquina virtual de toohello. 
2. Saudação de atalho **iniciar** menu e selecione **sistema**.
3. No menu à esquerda do hello, selecione **configurações avançadas do sistema**.
4. Em Olá **desempenho** seção, selecione **configurações**.
5. Selecione Olá **avançado** guia.
6. Em Olá **Memória Virtual** seção, selecione **alteração**.
7. Selecione Olá **C** unidade e, em seguida, clique em **Tamanho gerenciado pelo sistema** e, em seguida, clique em **definir**.
8. Selecione Olá **D** unidade e, em seguida, clique em **nenhum arquivo de paginação** e, em seguida, clique em **definir**.
9. Clique em Aplicar. Você receberá um aviso que computador Olá precisa toobe reiniciado para Olá alterações tootake efeito.
10. Reinicie a máquina virtual de saudação.

## <a name="change-hello-drive-letters"></a>Alterar Olá letras de unidade
1. Uma vez Olá VM reiniciar, faça logon novamente toohello VM.
2. Clique em Olá **iniciar** menu e tipo **diskmgmt.msc** e pressione Enter. O Gerenciamento de Disco será iniciado.
3. Clique duas vezes em **D**, Olá unidade de armazenamento temporário e selecione **alterar a letra da unidade e caminhos**.
4. Na Letra da unidade, selecione uma nova unidade como, por exemplo, **T** e clique em **OK**. 
5. Clique com botão direito no disco de dados hello e selecione **alterar a letra da unidade e caminhos**.
6. Na Letra da unidade, selecione a unidade **D** e clique em **OK**. 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a>Mova pagefile.sys unidade de armazenamento temporário de toohello back
1. Saudação de atalho **iniciar** menu e selecione **sistema**
2. No menu à esquerda do hello, selecione **configurações avançadas do sistema**.
3. Em Olá **desempenho** seção, selecione **configurações**.
4. Selecione Olá **avançado** guia.
5. Em Olá **Memória Virtual** seção, selecione **alteração**.
6. Selecione unidade Olá SO **C** e clique em **nenhum arquivo de paginação** e, em seguida, clique em **definir**.
7. Selecione a unidade de armazenamento temporário de saudação **T** e, em seguida, clique em **Tamanho gerenciado pelo sistema** e, em seguida, clique em **definir**.
8. Clique em **Aplicar**. Você receberá um aviso que computador Olá precisa toobe reiniciado para Olá alterações tootake efeito.
9. Reinicie a máquina virtual de saudação.

## <a name="next-steps"></a>Próximas etapas
* Você pode aumentar Olá armazenamento disponível tooyour máquina virtual [anexar um disco de dados adicionais](attach-managed-disk-portal.md).

