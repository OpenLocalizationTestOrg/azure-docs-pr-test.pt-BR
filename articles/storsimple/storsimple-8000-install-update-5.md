---
title: "aaaInstall atualização 5 em dispositivo da série StorSimple 8000 | Microsoft Docs"
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
ms.date: 08/22/2017
ms.author: alkohli
ms.openlocfilehash: a832f9953e8e39408efeeed375e3afe8eee8d0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-5-on-your-storsimple-device"></a>Instalar a Atualização 5 em seu dispositivo StorSimple

## <a name="overview"></a>Visão geral

Este tutorial explica como tooinstall atualização 5 em um dispositivo StorSimple executando uma versão anterior do software via Olá portal do Azure e usando o método de hotfix hello. método de hotfix Hello é usado quando um gateway é configurado em uma interface de rede diferente de DATA 0 do dispositivo do StorSimple hello e você está tentando tooupdate de uma versão de software 1 pré-atualização.

A Atualização 5 inclui o software de dispositivo, Storport e Spaceport, as atualizações de segurança do SO e as atualizações do SO, bem como atualizações de firmware de disco.  o software de dispositivo Hello, Spaceport, Storport, segurança e outras atualizações do sistema operacional são as atualizações sem interrupção. Olá sem interrupções ou regulares atualizações podem ser aplicadas por meio de saudação portal do Azure ou método de hotfix hello. atualizações de firmware de disco Olá atualizações precisam de interrupção e são aplicadas ao dispositivo hello está no modo de manutenção por meio do método de hotfix hello usando a interface do Windows PowerShell de saudação do dispositivo hello.

> [!IMPORTANT]
> * Um conjunto de pré-verificações de manuais e automáticas terminar instalação anterior toohello toodetermine integridade do dispositivo Olá em termos de conectividade de rede e estado do hardware. Essas pré-verificações de são executadas somente se você aplicar atualizações de saudação do hello portal do Azure.
> * É recomendável que você instale software hello e outras atualizações regulares via Olá portal do Azure. Você só deve ficar toohello do Windows PowerShell interface de dispositivo de saudação (tooinstall atualizações) se a verificação de pré-atualização gateway de saudação falhar no portal de saudação. Dependendo da versão de hello estiver atualizando a partir, Olá atualizações podem demorar 4 horas (ou superior) tooinstall. Olá atualizações do modo de manutenção devem ser instaladas por meio de interface do Windows PowerShell de saudação do dispositivo hello. Como as atualizações do modo de manutenção são atualizações que ocasionam interrupção, elas causam tempo de inatividade em seu dispositivo.
> * Se a execução hello opcional StorSimple Snapshot Manager, certifique-se de que você atualizou seu dispositivo de saudação do Gerenciador de instantâneos versão tooUpdate 5 tooupdating anterior.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-5-via-hello-azure-portal"></a>Instalar a atualização 5 via Olá portal do Azure
Executar seu dispositivo Olá seguindo as etapas tooupdate muito[atualização 5](storsimple-update5-release-notes.md).

> [!NOTE]
> Microsoft extrai informações de diagnóstico adicionais de dispositivo de saudação. Como resultado, quando a nossa equipe de operações identifica dispositivos que estão tendo problemas, estamos melhores toocollect equipado informações de dispositivo de saudação e diagnosticar problemas.

[!INCLUDE [storsimple-8000-install-update4-via-portal](../../includes/storsimple-8000-install-update5-via-portal.md)]

Verifique se seu dispositivo está executando a **Atualização 5 do StorSimple Série 8000 (6.3.9600.17845)**. Olá **Data da última atualização** devem ser modificados.

* Agora você verá que as atualizações do modo de manutenção de saudação estão disponíveis (essa mensagem pode continuar toobe exibido para o too24 horas após a instalação Olá atualizações). Atualizações do modo de manutenção são atualizações sem interrupção resultam em tempo de inatividade do dispositivo e só podem ser aplicadas por meio da interface do Windows PowerShell de saudação do seu dispositivo.

* Baixar atualizações do modo de manutenção hello usando Olá etapas listadas na [toodownload hotfixes](#to-download-hotfixes) toosearch para e baixar KB4011837, que instala atualizações de firmware de disco (hello outras atualizações já devem estar instaladas agora). Execute as etapas de saudação listadas na [instalar e verificar os hotfixes do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall Olá atualizações do modo de manutenção.

## <a name="install-update-5-as-a-hotfix"></a>Instalar a Atualização 5 como um hotfix


Olá versões de software que podem ser atualizadas usando o método de hotfix hello são:

* Atualização 0.1, 0.2, 0.3
* Atualização 1, 1.1, 1.2
* Atualização 2, 2.1, 2.2
* Atualização 3, 3.1
* Atualização 4

> [!NOTE] 
> Olá recomendado tooinstall do método que Update 5 é por meio de saudação portal do Azure. Use este procedimento se você não seleção de gateway Olá durante a tentativa de atualizações de saudação tooinstall por meio de saudação portal do Azure. verificação de saudação falha quando você tiver um gateway atribuído tooa dados não interface de rede 0 e o dispositivo está executando uma versão de software anteriores à atualização 1.

método de hotfix Hello envolve Olá três etapas a seguir:

1. Baixe Olá hotfixes do hello catálogo do Microsoft Update.
2. Instalar e verificar Olá hotfixes do modo normal.
3. Instalar e verifique se o hotfix do modo de manutenção hello.

#### <a name="download-updates-for-your-device"></a>Baixar atualizações para seu dispositivo

Você deve baixar e instalar Olá seguintes hotfixes no hello prescrita ordenar e Olá pastas sugeridas:

| Classificar | KB | Descrição | Tipo de atualização | Hora da instalação |Instalar na pasta|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4037264 |Atualização de software<br> Baixar o _HcsSfotwareUpdate.exe_ e o _CisMSDAgent.exe_ |Regular  <br></br>Não interruptiva |Aproxim. 25 minutos |FirstOrderUpdate|

Se a atualização de um dispositivo que executa a atualização 4, você só precisa atualizações cumulativas do sistema operacional tooinstall hello como atualizações de segunda ordem.

| Classificar | KB | Descrição | Tipo de atualização | Hora da instalação |Instalar na pasta|
| --- | --- | --- | --- | --- | --- |
| 2A. |KB4025336 |Pacote de atualizações cumulativas do SO <br> Baixar a versão Windows Server 2012 R2 |Regular  <br></br>Não interruptiva |- |SecondOrderUpdate|

Se a instalação de um dispositivo que executa a atualização 3 ou anterior, instale Olá além de seguir as atualizações cumulativas toohello.

| Classificar | KB | Descrição | Tipo de atualização | Hora da instalação |Instalar na pasta|
| --- | --- | --- | --- | --- | --- |
| 2B. |KB4011841 <br> KB4011842 |Atualizações de firmware e driver LSI <br> Atualização de firmware USM (versão 3.38) |Regular  <br></br>Não interruptiva |Aproxim. 3 horas <br> (inclui 2A. + 2B. + 2C.)|SecondOrderUpdate|
| 2C. |KB3139398 <br> KB3142030 <br> KB3108381 <br> KB3153704 <br> KB3174644 <br> KB3139914   |Pacote de atualizações de segurança do SO <br> Baixar a versão Windows Server 2012 R2 |Regular  <br></br>Não interruptiva |- |SecondOrderUpdate|
| 2D. |KB3146621 <br> KB3103616 <br> KB3121261 <br> KB3123538 |Pacote de atualizações do SO <br> Baixar a versão Windows Server 2012 R2 |Regular  <br></br>Não interruptiva |- |SecondOrderUpdate|


Talvez também seja necessário tooinstall atualizações de firmware de disco na parte superior de todas as atualizações de saudação mostradas no hello tabelas anteriores. Você pode verificar se você precisa Olá atualizações de firmware de disco executando Olá `Get-HcsFirmwareVersion` cmdlet. Se você estiver executando essas versões de firmware: `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N003`, `0107`, em seguida, você não precisa tooinstall essas atualizações.

| Classificar | KB | Descrição | Tipo de atualização | Hora da instalação | Instalar na pasta|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4037263 |Firmware de disco |Manutenção  <br></br>Interruptiva |~ 30 Min. | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Se a atualização da atualização 4, tempo de instalação total de saudação é fechar too4 horas.
> * Antes de usar este Olá tooapply de procedimento de atualização, certifique-se de que ambos os controladores de dispositivo Olá estão online e todos os componentes de hardware Olá estão íntegros.

Executar Olá toodownload as etapas a seguir e instalar os hotfixes hello.

[!INCLUDE [storsimple-install-update5-hotfix](../../includes/storsimple-install-update5-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá [versão de atualização 5](storsimple-update5-release-notes.md).

