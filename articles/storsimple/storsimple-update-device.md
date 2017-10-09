---
title: aaaUpdate seu dispositivo StorSimple | Microsoft Docs
description: "Explica como atualizar o hello toouse StorSimple recurso tooinstall regular e atualizações do modo de manutenção e hotfixes."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a>Atualizar seu dispositivo do StorSimple série 8000
## <a name="overview"></a>Visão geral
Olá StorSimple atualizações recursos permitem que você tooeasily manter atualizado o seu dispositivo StorSimple. Dependendo do tipo de atualização Olá, você pode aplicar o dispositivo toohello de atualizações por meio de saudação portal clássico do Azure ou por meio da interface do Windows PowerShell hello. Este tutorial descreve os tipos de atualização de saudação e como tooinstall cada um deles.

Você pode aplicar dois tipos de atualização de dispositivo: 

* Atualizações regulares (ou modo Normal)
* Atualizações no modo de Manutenção

Você pode instalar atualizações regulares via Olá portal clássico do Azure ou o Windows PowerShell; No entanto, você deve usar o Windows PowerShell tooinstall atualizações do modo de manutenção. 

Cada tipo de atualização será descrito separadamente a seguir.

### <a name="regular-updates"></a>Atualizações regulares
As atualizações regulares são atualizações sem interrupção que podem ser instaladas quando o dispositivo hello está no modo Normal. Essas atualizações são aplicadas por meio do controlador do dispositivo Olá Microsoft Update site tooeach. 

> [!IMPORTANT]
> Um failover de controlador pode ocorrer durante o processo de atualização de saudação. No entanto, isso não afetará a disponibilidade do sistema ou a operação.
> 
> 

* Para obter detalhes sobre como tooinstall regular atualiza via Olá portal clássico do Azure, consulte [instalar atualizações regulares via Olá portal clássico do Azure](#install-regular-updates-via-the-azure-classic-portal).
* Você também pode instalar atualizações regulares por meio do Windows PowerShell para StorSimple. Para obter detalhes, consulte [Instalar atualizações regulares por meio do Windows PowerShell para StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).

### <a name="maintenance-mode-updates"></a>Atualizações no modo de Manutenção
As atualizações do Modo de Manutenção são atualizações com interrupção, como atualizações de firmware de disco. Essas atualizações exigem Olá dispositivo toobe colocar em modo de manutenção. Para obter detalhes, consulte [Etapa 2: Entrar no modo de Manutenção](#step2). Você não pode usar as atualizações do modo de manutenção do hello tooinstall de portal clássico do Azure. Em vez disso, você deverá usar o Windows PowerShell para StorSimple. 

Para obter detalhes sobre como o modo de manutenção tooinstall atualizações, consulte [atualizações do modo de manutenção instalar por meio do Windows PowerShell para StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).

> [!IMPORTANT]
> Modo de manutenção, as atualizações devem ser aplicadas separadamente tooeach controlador. 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a>Instalar as atualizações regulares via Olá portal clássico do Azure
Você pode usar o dispositivo StorSimple de tooyour de atualizações do hello tooapply de portal clássico do Azure.

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a>Instalar atualizações regulares por meio do Windows PowerShell para StorSimple
Como alternativa, você pode usar o Windows PowerShell para atualizações do StorSimple tooapply regular (modo Normal).

> [!IMPORTANT]
> Embora você possa instalar atualizações regulares usando o Windows PowerShell para StorSimple, é altamente recomendável que você instale atualizações regulares por meio de saudação portal clássico do Azure. Começando com atualização 1, pré-verificações de será executada tooinstalling anterior atualizações do portal de saudação. Essas verificações evitarão falhas e garantirão uma experiência mais uniforme. 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>Instalar atualizações do modo de Manutenção instalar por meio do Windows PowerShell para StorSimple
Usar o Windows PowerShell para StorSimple tooapply manutenção modo atualizações tooyour o dispositivo StorSimple. Todas as solicitações de E/S são pausadas neste modo. Serviços, como a memória de acesso aleatório não volátil (NVRAM) ou Olá serviço também são interrompidos. Ambos os controladores são reiniciados quando você entra ou sai desse modo. Quando você sair deste modo, todos os serviços de saudação serão retomada e devem ser íntegros. (Isso pode levar alguns minutos).

Se você precisar tooapply atualizações do modo de manutenção, você receberá um alerta por meio de saudação portal clássico do Azure que você possui atualizações que devem ser instaladas. Esse alerta inclui instruções sobre como usar o Windows PowerShell para atualizações do StorSimple tooinstall hello. Depois de atualizar seu dispositivo, use Olá mesmo modo tooRegular do procedimento toochange Olá dispositivo. Para obter instruções passo a passo, consulte [Etapa 4: Sair do modo de Manutenção](#step4).

> [!IMPORTANT]
> * Antes de entrar no modo de manutenção, verifique se ambos os controladores estão íntegros verificando Olá **Status do Hardware** em Olá **manutenção** página Olá portal clássico do Azure. Se o controlador de saudação não está íntegro, entre em contato com o Microsoft Support para as próximas etapas hello. Para obter mais informações, acesse tooContact Microsoft Support. 
> * Quando você estiver no modo de manutenção, é necessário tooapply Olá atualização pela primeira vez em um controlador e, em seguida, em Olá outro controlador.
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a>Etapa 1: Conectar o console serial toohello<a name="step1">
Primeiro, use um aplicativo, como o PuTTY tooaccess Olá console serial. Olá procedimento a seguir explica como console serial do toohello toouse tooconnect PuTTY.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a>Etapa 2: Entrar no modo de Manutenção <a name="step2">
Depois de conectar o console toohello, determinar se há atualizações tooinstall e insira tooinstall do modo de manutenção-los.

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a>Etapa 3: Instalar as atualizações <a name="step3">
Em seguida, instale as atualizações.

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a>Etapa 4: Sair do modo de Manutenção <a name="step4">
Por fim, saia do modo de Manutenção.

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a>Instale correções por meio do Windows PowerShell para StorSimple
Ao contrário de atualizações para o Microsoft Azure StorSimple, os hotfixes são instalados de uma pasta compartilhada. Assim como acontece com as atualizações, há dois tipos de hotfixes: 

* Hotfixes regulares 
* Hotfixes no modo de Manutenção  

Olá procedimentos a seguir explicam como toouse do Windows PowerShell para StorSimple tooinstall regular e hotfixes do modo de manutenção.

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a>O que acontece tooupdates se você executar uma fábrica de redefinição do dispositivo Olá?
Se um dispositivo for toofactory de redefinir as configurações, todas as atualizações de saudação serão perdidas. Depois que o dispositivo de redefinição de fábrica Olá é registrado e configurado, você precisará toomanually instalar as atualizações por meio de saudação portal clássico do Azure e/ou do Windows PowerShell para StorSimple. Para obter mais informações sobre a redefinição de fábrica, consulte [redefinir as configurações padrão do hello dispositivo toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [usando o Windows PowerShell para StorSimple tooadminister seu dispositivo StorSimple](storsimple-windows-powershell-administration.md).
* Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-manager-service-administration.md).

