---
title: "aaaInstall atualização 2 em seu dispositivo StorSimple | Microsoft Docs"
description: "Explica como tooinstall StorSimple 8000 Series atualização 2 em seu dispositivo da série StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8c8981df-75d9-4d19-b137-d6c6ba39dcfb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 33a0bea4358c944644563192f686af332d2ad7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a>Instalar a Atualização 2 no dispositivo StorSimple
## <a name="overview"></a>Visão geral
Este tutorial explica como tooinstall atualização 2 em um dispositivo StorSimple executando uma versão anterior do software via Olá portal clássico do Azure. tutorial Olá também aborda etapas Olá necessárias para atualização hello quando um gateway é configurado em uma interface de rede diferente de DATA 0 do dispositivo do StorSimple hello e você está tentando tooupdate de uma versão de software 1 pré-atualização.

A Atualização 2 inclui atualizações de software do dispositivo, atualizações do driver LSI e atualizações de firmware de disco. Olá dispositivo atualizações de software e LSI atualizações sem interrupções e podem ser aplicadas por meio de saudação portal clássico do Azure. atualizações de firmware de disco Olá atualizações precisam de interrupção e só podem ser aplicadas por meio da interface do Windows PowerShell saudação do dispositivo de saudação.

> [!IMPORTANT]
> * Você não poderá ver a atualização 2 imediatamente porque fazemos uma distribuição em fases de saudação atualizações. Procure novamente as atualizações em poucos dias, uma vez que elas serão disponibilizadas em breve.
> * Um conjunto de pré-verificações de manuais e automáticas terminar instalação anterior toohello toodetermine integridade do dispositivo Olá em termos de conectividade de rede e estado do hardware. Essas pré-verificações de são executadas somente se você aplicar atualizações de saudação do hello portal clássico do Azure.
> * É recomendável que você instalar o software de saudação e atualizações de driver via Olá portal clássico do Azure. Você só deve ficar toohello do Windows PowerShell interface de dispositivo de saudação (tooinstall atualizações) se a verificação de pré-atualização gateway de saudação falhar no portal de saudação. Olá atualizações podem levar horas de 4 a 7 tooinstall (incluindo Olá atualizações do Windows). Olá atualizações do modo de manutenção devem ser instaladas por meio de interface do Windows PowerShell de saudação do dispositivo hello. Como as atualizações do modo de manutenção são atualizações com interrupção, elas resultarão em um tempo de inatividade para seu dispositivo.
> * Se a execução hello opcional StorSimple Snapshot Manager, certifique-se de que você atualizou seu dispositivo de saudação do Gerenciador de instantâneos versão tooUpdate 2 tooupdating anterior.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-hello-azure-classic-portal"></a>Instale a atualização 2 via Olá portal clássico do Azure
Executar seu dispositivo Olá seguindo as etapas tooupdate muito[atualização 2](storsimple-update2-release-notes.md).

> [!NOTE]
> Atualização 2 permite que a Microsoft toopull informações adicionais de diagnóstico de dispositivo de saudação. Como resultado, quando a nossa equipe de operações identifica dispositivos que estão tendo problemas, estamos melhores toocollect equipado informações de dispositivo de saudação e diagnosticar problemas. Aceitando a atualização 2, nos permite tooprovide esse suporte proativo.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Verifique se o dispositivo está executando a **Atualização 2 do StorSimple Série 8000 (6.3.9600.17673)**. Olá **Data da última atualização** também deve ser modificado. Você verá que as atualizações do modo de manutenção estão disponíveis (essa mensagem pode continuar toobe exibido para o too24 horas após a instalação Olá atualizações).
   
   Atualizações do modo de manutenção são atualizações sem interrupção resultam em tempo de inatividade do dispositivo e só podem ser aplicadas por meio da interface do Windows PowerShell de saudação do seu dispositivo. Em alguns casos quando você estiver executando a atualização 1.2, o firmware de disco já pode ser atualizado, caso em que você não precisa tooinstall atualizações de qualquer modo de manutenção.
2. Baixar atualizações do modo de manutenção hello usando Olá etapas listadas na [toodownload hotfixes](#to-download-hotfixes) toosearch para e baixar KB3121899, que instala atualizações de firmware de disco (hello outras atualizações já devem estar instaladas agora).
3. Execute as etapas de saudação listadas na [instalar e verificar os hotfixes do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall Olá atualizações do modo de manutenção.

## <a name="install-update-2-as-a-hotfix"></a>Instalar a Atualização 2 como um hotfix
Use este procedimento se você não seleção de gateway Olá durante a tentativa de atualizações de saudação tooinstall por meio de saudação portal clássico do Azure. verificação de Olá falha e você tiver um gateway atribuído tooa dados não interface de rede 0 e o dispositivo está executando um software versão anterior tooUpdate 1.

versões de software de saudação que podem ser atualizadas usando o método de hotfix hello são atualização 0,1, atualização 0,2 e atualização 0.3, atualização 1, atualização 1.1 e 1.2 de atualização. método de hotfix Hello envolve Olá três etapas a seguir:

* Baixe Olá hotfixes do hello catálogo do Microsoft Update.
* Instalar e verificar Olá hotfixes do modo normal.
* Instalar e verifique se o hotfix do modo de manutenção hello.

tooinstall atualização 2, como um hotfix, você deve baixar e instalar Olá hotfixes a seguir:

| Classificar | KB | Descrição | Tipo de atualização |
| --- | --- | --- | --- |
| 1 |KB3121901 |Atualização de software |Regular |
| 2 |KB3121900 |Driver LSI |Regular |
| 3 |KB3080728 |Correção do Storport  </br> Windows Server 2012 R2 |Regular |
| 4 |KB3090322 |Correção do Spaceport  </br> Windows Server 2012 R2 |Regular |
| 5 |KB3121899 |Firmware de disco |Manutenção  |

> [!IMPORTANT]
> * Se o dispositivo está executando a versão de lançamento (GA), entre em contato com [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist com hello atualizar.
> * Toobe de necessidades esse procedimento executadas apenas uma vez tooapply atualização 2. Você pode usar as atualizações subsequentes Olá tooapply de portal clássico do Azure.
> * Cada instalação de hotfix pode levar cerca de 20 minutos toocomplete. Tempo de instalação total é fechar too2 horas.
> * Antes de usar este Olá tooapply de procedimento de atualização, certifique-se de que ambos os controladores estejam online e todos os componentes de hardware Olá estão íntegros.
> 
> 

Execute essa atualização de saudação tooapply as etapas a seguir como um hotfix.

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá [atualização 2 versão](storsimple-update2-release-notes.md).

