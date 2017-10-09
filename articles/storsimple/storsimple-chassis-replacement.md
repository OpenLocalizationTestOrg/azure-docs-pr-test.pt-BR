---
title: "chassi aaaReplace no dispositivo da série StorSimple 8000 | Microsoft Docs"
description: "Descreve como tooremove e substituir Olá chassi do compartimento principal do StorSimple ou compartimento EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8576d63520a6f7d3267180d2a68d4fc38fd48fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a>Substitua o chassi Olá em seu dispositivo StorSimple
## <a name="overview"></a>Visão geral
Este tutorial explica como tooremove e substituir um chassi em um dispositivo da série StorSimple 8000. modelo de saudação StorSimple 8100 é um dispositivo de compartimento simples (um chassi), enquanto Olá 8600 é um dispositivo de compartimento duplo (dois chassis). Para um modelo 8600, há potencialmente dois chassis que podem falhar em dispositivo Olá: Olá chassi do compartimento principal hello ou chassi Olá Olá compartimento EBOD.

Em ambos os casos, o chassi de substituição de saudação que é fornecido pela Microsoft está vazio. Não será incluído nenhum módulos de energia e resfriamento (PCM), módulo de controlador, unidade de disco de estado sólido (SSD), unidade de disco rígido (HD) ou módulos EBOD.

> [!IMPORTANT]
> Antes de remover e substituir o chassi hello, revise as informações de segurança de Olá em [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="remove-hello-chassis"></a>Remover o chassi Olá
Execute Olá chassi de saudação do tooremove as etapas a seguir em seu dispositivo StorSimple.

#### <a name="tooremove-a-chassis"></a>tooremove um chassi
1. Verifique se o dispositivo StorSimple Olá é desligado e desconectado de todas as fontes de alimentação hello.
2. Remova todos os cabos SAS e rede hello, se aplicável.
3. Remova a unidade de saudação do rack hello.
4. Remova cada uma das unidades hello e observe os slots de saudação do qual eles serão removidos. Para obter mais informações, consulte [remover a unidade de disco Olá](storsimple-disk-drive-replacement.md#remove-the-disk-drive).
5. No hello compartimento EBOD (se esse for o chassi Olá que falhou), remova módulos do controlador EBOD hello. Para obter mais informações, consulte [Remover um controlador EBOD](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller). 
   
    No hello compartimento principal (se esse for o chassi Olá que falhou), remova Olá controladores e observe os slots de saudação do qual eles serão removidos. Para obter mais informações, consulte [Remover um controlador](storsimple-controller-replacement.md#remove-a-controller).

## <a name="install-hello-chassis"></a>Instalar o chassi Olá
Execute Olá chassi de saudação do tooinstall as etapas a seguir em seu dispositivo StorSimple.

#### <a name="tooinstall-a-chassis"></a>tooinstall um chassi
1. Monte o chassi Olá em rack hello. Para saber mais, confira [Montar em rack o dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) ou [Montar em rack o dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).
2. Depois de saudação chassi estiver montado no rack hello, instale módulos do controlador Olá no hello que mesmas posições que estavam instaladas anteriormente no.
3. Olá instalar unidades em Olá mesmo posiciona e slots que elas estavam instaladas anteriormente no.
   
   > [!NOTE]
   > É recomendável que você instala Olá SSDs nos slots de saudação primeiro e, em seguida, instala Olá HDDs.
   > 
   > 
4. Com hello dispositivo montado no rack hello e componentes Olá instalados, se conectar a fontes de alimentação apropriadas de toohello seu dispositivo e Ativar dispositivo hello. Para obter detalhes, confira [Cabear o dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) ou [Cabear o dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).

