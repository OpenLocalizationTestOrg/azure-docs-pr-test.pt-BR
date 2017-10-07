---
title: "aaaInstall atualização 4 no dispositivo da série StorSimple 8000 | Microsoft Docs"
description: "Explica como tooinstall StorSimple 8000 Series atualização 4 no seu dispositivo da série StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/02/2017
ms.author: alkohli
ms.openlocfilehash: 3507edbde5e6e43b6c450bfea19494d47b5a5ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-4-on-your-storsimple-device"></a>Instalar a Atualização 4 em seu dispositivo StorSimple

## <a name="overview"></a>Visão geral

Este tutorial explica como tooinstall atualização 4 em um dispositivo StorSimple executando uma versão anterior do software via Olá portal do Azure e usando o método de hotfix hello. método de hotfix Hello é usado quando um gateway é configurado em uma interface de rede diferente de DATA 0 do dispositivo do StorSimple hello e você está tentando tooupdate de uma versão de software 1 pré-atualização.

A Atualização 4 inclui atualizações de segurança do SO, do software do dispositivo, do firmware USM, de driver e firmware LSI, do Storport e Spaceport, bem como um host de outras atualizações do SO.  o software de dispositivo Hello, firmware USM, Spaceport, Storport e outras atualizações do sistema operacional são as atualizações sem interrupção. Olá sem interrupções ou regulares atualizações podem ser aplicadas por meio de saudação portal do Azure ou método de hotfix hello. atualizações de firmware de disco Olá atualizações precisam de interrupção e só podem ser aplicadas por meio do método de hotfix hello usando a interface do Windows PowerShell de saudação do dispositivo hello.

> [!IMPORTANT]
> * Um conjunto de pré-verificações de manuais e automáticas terminar instalação anterior toohello toodetermine integridade do dispositivo Olá em termos de conectividade de rede e estado do hardware. Essas pré-verificações de são executadas somente se você aplicar atualizações de saudação do hello portal do Azure.
> * É recomendável que você instale software hello e outras atualizações regulares via Olá portal do Azure. Você só deve ficar toohello do Windows PowerShell interface de dispositivo de saudação (tooinstall atualizações) se a verificação de pré-atualização gateway de saudação falhar no portal de saudação. Dependendo da versão de hello estiver atualizando a partir, Olá atualizações podem demorar 4 horas (ou superior) tooinstall. Olá atualizações do modo de manutenção também devem ser instaladas por meio de interface do Windows PowerShell de saudação do dispositivo hello. Como as atualizações do modo de manutenção são atualizações com interrupção, elas resultarão em um tempo de inatividade para seu dispositivo.
> * Se a execução hello opcional StorSimple Snapshot Manager, certifique-se de que você atualizou seu dispositivo de saudação do Gerenciador de instantâneos versão tooUpdate 4 tooupdating anterior.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-4-via-hello-azure-portal"></a>Instalar a atualização 4 via Olá portal do Azure
Executar seu dispositivo Olá seguindo as etapas tooupdate muito[atualização 4](storsimple-update4-release-notes.md).

> [!NOTE]
> Microsoft extrai informações de diagnóstico adicionais de dispositivo de saudação. Como resultado, quando a nossa equipe de operações identifica dispositivos que estão tendo problemas, estamos melhores toocollect equipado informações de dispositivo de saudação e diagnosticar problemas. 

[!INCLUDE [storsimple-8000-install-update4-via-portal](../../includes/storsimple-8000-install-update4-via-portal.md)]

Verifique se o dispositivo está executando a **Atualização 4 do StorSimple série 8000 (6.3.9600.17820)**. Olá **Data da última atualização** também deve ser modificado.

* Agora você verá que as atualizações do modo de manutenção de saudação estão disponíveis (essa mensagem pode continuar toobe exibido para o too24 horas após a instalação Olá atualizações). Atualizações do modo de manutenção são atualizações sem interrupção resultam em tempo de inatividade do dispositivo e só podem ser aplicadas por meio da interface do Windows PowerShell de saudação do seu dispositivo.

* Baixar atualizações do modo de manutenção hello usando Olá etapas listadas na [toodownload hotfixes](#to-download-hotfixes) toosearch para e baixar KB4011837, que instala atualizações de firmware de disco (hello outras atualizações já devem estar instaladas agora). Execute as etapas de saudação listadas na [instalar e verificar os hotfixes do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall Olá atualizações do modo de manutenção.

## <a name="install-update-4-as-a-hotfix"></a>Instalar a Atualização 4 como um hotfix
Olá recomendado tooinstall do método que Update 4 é por meio de saudação portal do Azure.

Use este procedimento se você não seleção de gateway Olá durante a tentativa de atualizações de saudação tooinstall por meio de saudação portal do Azure. verificação de Olá falha e você tiver um gateway atribuído tooa dados não interface de rede 0 e o dispositivo está executando um software versão anterior tooUpdate 1.

Olá versões de software que podem ser atualizadas usando o método de hotfix hello são:

* Atualização 0.1, 0.2, 0.3
* Atualização 1, 1.1, 1.2
* Atualização 2, 2.1, 2.2
* Atualização 3, 3.1


método de hotfix Hello envolve Olá três etapas a seguir:

1. Baixe Olá hotfixes do hello catálogo do Microsoft Update.
2. Instalar e verificar Olá hotfixes do modo normal.
3. Instalar e verifique se o hotfix do modo de manutenção hello.

#### <a name="download-updates-for-your-device"></a>Baixar atualizações para seu dispositivo

Você deve baixar e instalar Olá seguintes hotfixes no hello prescrita ordenar e Olá pastas sugeridas:

| Classificar | KB | Descrição | Tipo de atualização | Hora da instalação |Instalar na pasta|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4011839 |Atualização de software |Regular  <br></br>Não interruptiva |Aproxim. 25 minutos |FirstOrderUpdate|
| 2A. |KB4011841 <br> KB4011842 |Atualizações de firmware e driver LSI <br> Atualização de firmware USM (versão 3.38) |Regular  <br></br>Não interruptiva |Aproxim. 3 horas <br> (inclui 2A. + 2B. + 2C.)|SecondOrderUpdate|
| 2B. |KB3139398, KB3108381 <br> KB3205400, KB3142030 <br> KB3197873, KB3197873 <br> KB3192392, KB3153704 <br> KB3174644, KB3139914  |Pacote de atualizações de segurança do SO <br> Baixar o Windows Server 2012 R2 |Regular  <br></br>Não interruptiva |- |SecondOrderUpdate|
| 2C. |KB3210083, KB3103616 <br> KB3146621, KB3121261 <br> KB3123538 |Pacote de atualizações do SO <br> Baixar o Windows Server 2012 R2 |Regular  <br></br>Não interruptiva |- |SecondOrderUpdate|

Talvez também seja necessário tooinstall atualizações de firmware de disco na parte superior de todas as atualizações de saudação mostradas no hello tabelas anteriores. Você pode verificar se você precisa Olá atualizações de firmware de disco executando Olá `Get-HcsFirmwareVersion` cmdlet. Se você estiver executando essas versões de firmware: `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N002`, `0106`, em seguida, você não precisa tooinstall essas atualizações.

| Classificar | KB | Descrição | Tipo de atualização | Hora da instalação | Instalar na pasta|
| --- | --- | --- | --- | --- | --- |
| 3. |KB3121899 |Firmware de disco |Manutenção  <br></br>Interruptiva |~ 30 Min. | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Toobe de necessidades esse procedimento executadas apenas uma vez tooapply atualização 4. Você pode usar as atualizações subsequentes Olá tooapply portal do Azure.
> * Se a atualização da atualização 3 ou 3.1, tempo de instalação total de saudação é fechar too4 horas.
> * Antes de usar este Olá tooapply de procedimento de atualização, certifique-se de que ambos os controladores de dispositivo Olá estão online e todos os componentes de hardware Olá estão íntegros.

Executar Olá toodownload as etapas a seguir e instalar os hotfixes hello.

[!INCLUDE [storsimple-install-update4-hotfix](../../includes/storsimple-install-update4-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá [atualização 4 versão](storsimple-update4-release-notes.md).

