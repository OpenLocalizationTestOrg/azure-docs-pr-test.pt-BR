---
title: "aaaInstall 2.2 atualização em seu dispositivo StorSimple | Microsoft Docs"
description: "Explica como tooinstall StorSimple 8000 Series atualização 2.2 no seu dispositivo da série StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 047c7a4b-73d0-45ea-8d51-c54d71871392
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/02/2016
ms.author: alkohli
ms.openlocfilehash: cedb83ce42bc6bb81a4e43345da3f25b71036d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-22-on-your-storsimple-device"></a>Instalar a Atualização 2.2 no dispositivo StorSimple
## <a name="overview"></a>Visão geral
Este tutorial explica como tooinstall atualização 2.2 em um dispositivo StorSimple executando uma versão anterior do software via Olá portal clássico do Azure e usando o método de hotfix hello. método de hotfix Hello é usado quando um gateway é configurado em uma interface de rede diferente de DATA 0 do dispositivo do StorSimple hello e você está tentando tooupdate de uma versão de software 1 pré-atualização.

A Atualização 2.2 inclui o software do dispositivo, o WMI e as atualizações do iSCSI. Se atualizar da versão 2.1, atualização de software do dispositivo Olá somente será necessário toobe aplicado. Se estiver atualizando de uma versão de pré-atualização 2, também será necessário tooapply LSI driver, Spaceport, Storport e atualizações de firmware de disco. Olá software de dispositivo, WMI, iSCSI, driver LSI, Spaceport e Storport correções atualizações sem interrupções e podem ser aplicadas por meio de saudação portal clássico do Azure. atualizações de firmware de disco Olá atualizações precisam de interrupção e só podem ser aplicadas por meio da interface do Windows PowerShell saudação do dispositivo de saudação. 

> [!IMPORTANT]
> * Um conjunto de pré-verificações de manuais e automáticas terminar instalação anterior toohello toodetermine integridade do dispositivo Olá em termos de conectividade de rede e estado do hardware. Essas pré-verificações de são executadas somente se você aplicar atualizações de saudação do hello portal clássico do Azure.
> * É recomendável que você instalar o software de saudação e atualizações de driver via Olá portal clássico do Azure. Você só deve ficar toohello do Windows PowerShell interface de dispositivo de saudação (tooinstall atualizações) se a verificação de pré-atualização gateway de saudação falhar no portal de saudação. Dependendo da versão de hello que estiver atualizando a partir, Olá atualizações podem demorar tooinstall 1.5-2,5 horas. Olá atualizações do modo de manutenção devem ser instaladas por meio de interface do Windows PowerShell de saudação do dispositivo hello. Como as atualizações do modo de manutenção são atualizações com interrupção, elas resultarão em um tempo de inatividade para seu dispositivo.
> * Se a execução hello opcional StorSimple Snapshot Manager, certifique-se de que você atualizou seu dispositivo de saudação do Gerenciador de instantâneos versão tooUpdate 2.2 tooupdating anterior.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-22-via-hello-azure-classic-portal"></a>Instalar atualização 2.2 via Olá portal clássico do Azure
Executar seu dispositivo Olá seguindo as etapas tooupdate muito[atualização 2.2](storsimple-update21-release-notes.md).

> [!NOTE]
> Se você estiver aplicando a atualização 2 ou posterior (incluindo atualização 2.1), a Microsoft será capaz de toopull informações adicionais de diagnóstico de dispositivo de saudação. Como resultado, quando a nossa equipe de operações identifica dispositivos que estão tendo problemas, estamos melhores toocollect equipado informações de dispositivo de saudação e diagnosticar problemas. Aceitando a atualização 2 ou posterior, nos permite tooprovide esse suporte proativo.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Verifique se o dispositivo está executando a **Atualização 2.2 do StorSimple Série 8000 (6.3.9600.17708)**. Olá **Data da última atualização** também deve ser modificado. 
   
   Se você estiver atualizando de uma tooUpdate anterior da versão 2, você também verá que as atualizações do modo de manutenção de saudação estão disponíveis (essa mensagem pode continuar toobe exibido para o too24 horas após a instalação Olá atualizações).
   
   Atualizações do modo de manutenção são atualizações sem interrupção resultam em tempo de inatividade do dispositivo e só podem ser aplicadas por meio da interface do Windows PowerShell de saudação do seu dispositivo. Em alguns casos quando você estiver executando a atualização 1.2, o firmware de disco já pode ser atualizado, caso em que você não precisa tooinstall atualizações de qualquer modo de manutenção.
   
   Se você estiver atualizando da Atualização 2, seu dispositivo agora deverá estar atualizado. Você pode ignorar Olá restantes etapas.
2. Baixar atualizações do modo de manutenção hello usando Olá etapas listadas na [toodownload hotfixes](#to-download-hotfixes) toosearch para e baixar KB3121899, que instala atualizações de firmware de disco (hello outras atualizações já devem estar instaladas agora).
3. Execute as etapas de saudação listadas na [instalar e verificar os hotfixes do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall Olá atualizações do modo de manutenção. 

## <a name="install-update-22-as-a-hotfix"></a>Instalar a Atualização 2.2 como um hotfix
Use este procedimento se você não seleção de gateway Olá durante a tentativa de atualizações de saudação tooinstall por meio de saudação portal clássico do Azure. verificação de Olá falha e você tiver um gateway atribuído tooa dados não interface de rede 0 e o dispositivo está executando um software versão anterior tooUpdate 1.

Olá versões de software que podem ser atualizadas usando o método de hotfix hello são:

* Atualização 0.1, 0.2, 0.3
* Atualização 1, 1.1, 1.2
* Atualização 2, 2.1 

> [!IMPORTANT]
> * Se o dispositivo está executando a versão de lançamento (GA), entre em contato com [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist com hello atualizar.
> 
> 

método de hotfix Hello envolve Olá três etapas a seguir:

* Baixe Olá hotfixes do hello catálogo do Microsoft Update.
* Instalar e verificar Olá hotfixes do modo normal.
* Instalar e verifique se o hotfix do modo de manutenção hello (somente quando a atualização de software de pré-atualização 2).

#### <a name="download-updates-for-a-device-running-update-21-software"></a>Baixe as atualizações para um dispositivo que executa o software da Atualização 2.1
**Se o dispositivo está executando a atualização 2.1**, você deve baixar a atualização de software de dispositivo de saudação somente KB3179904. Instale somente o arquivo binário de saudação precedido de 'all hcsmdssoftwareudpate'. Não instale Olá Cis e atualização do agente MDS Olá precedidos de `all-cismdsagentupdatebundle`. Falha toodo portanto resultará em erro. Esta é uma atualização sem interrupção, e/s não serão interrompidas e dispositivo Olá não terá nenhum tempo de inatividade.

#### <a name="download-updates-for-a-device-running-update-2-software"></a>Baixe as atualizações para um dispositivo que executa o software da Atualização 2
**Se o dispositivo está executando a atualização 2**, você deve baixar e instalar Olá hotfixes no hello prescrita ordem a seguir:

| Classificar | KB | Descrição | Tipo de atualização | Hora da instalação |
| --- | --- | --- | --- | --- |
| 1. |KB3179904 |Atualização de software &#42; |Regular  <br></br>Não interruptiva |~ 45 Min. |
| 2. |KB3146621 |Pacote iSCSI |Regular  <br></br>Não interruptiva |~ 20 Min. |
| 3. |KB3103616 |Pacote WMI |Regular  <br></br>Não interruptiva |~ 12 Min. |

 &#42;  *Observe, atualização de software consiste em dois arquivos binários: precedidos de atualização de software de dispositivo de `all-hcsmdssoftwareupdate` Olá Cis e agente do Mds precedidos de `all-cismdsagentupdatebundle`. atualização de software de dispositivo Olá deve ser instalada antes do agente Olá Cis e Mds. Também será preciso reiniciar o controlador ativo do hello via Olá `Restart-HcsController` cmdlet após a aplicação de hello Cis e atualização do agente MDS (e antes de aplicar Olá restantes atualizações).* 

#### <a name="download-updates-for-a-device-running-pre-update-2-software"></a>Baixe as atualizações para um dispositivo que executa um software anterior à Atualização 2
**Se o dispositivo está executando versões 0.2, 0.3, 1.0 e 1.1**, você deve baixar e instalar Olá LSI driver e firmware atualizar além toohello software, iSCSI e atualizações WMI. Se você estiver executando a Atualização 1.2 ou 2, essa atualização já estará instalada. 

| Classificar | KB | Descrição | Tipo de atualização | Hora da instalação |
| --- | --- | --- | --- | --- |
| 4. |KB3121900 |Driver LSI e firmware |Regular  <br></br>Não interruptiva |~ 20 Min. |

<br></br>
**Se o dispositivo está executando versões 0.2, 0.3, 1.0, 1.1 e 1.2**, você deve baixar e instalar hello Spaceport e correção de Storport hello. Se você estiver executando a Atualização 2, eles já estarão instalados.

| Classificar | KB | Descrição | Tipo de atualização | Hora da instalação |
| --- | --- | --- | --- | --- |
| 5. |KB3090322 |Correção do Spaceport  </br> Windows Server 2012 R2 |Regular  <br></br>Não interruptiva |~ 20 Min. |
| 6. |KB3080728 |Correção do Storport  </br> Windows Server 2012 R2 |Regular  <br></br>Não interruptiva |~ 20 Min. |

<br></br>
Talvez também seja necessário tooinstall atualizações de firmware de disco. Você pode verificar se você precisa Olá atualizações de firmware de disco executando Olá `Get-HcsFirmwareVersion` cmdlet. Se você estiver executando essas versões de firmware: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, em seguida, você não precisa tooinstall essas atualizações.

| Classificar | KB | Descrição | Tipo de atualização | Hora da instalação |
| --- | --- | --- | --- | --- |
| 7. |KB3121899 |Firmware de disco |Manutenção  <br></br>Interruptiva |~ 30 Min. |

<br></br>

> [!IMPORTANT]
> * Toobe de necessidades esse procedimento executadas apenas uma vez tooapply 2.2 de atualização. Você pode usar as atualizações subsequentes Olá tooapply de portal clássico do Azure.
> * Se estiver atualizando de atualização 2, tempo de instalação total de saudação é fechar too1.5 horas.
> * Antes de usar este Olá tooapply de procedimento de atualização, certifique-se de que ambos os controladores de dispositivo Olá estão online e todos os componentes de hardware Olá estão íntegros.
> 
> 

Executar Olá toodownload as etapas a seguir e instalar os hotfixes hello.

[!INCLUDE [storsimple-install-update21-hotfix](../../includes/storsimple-install-update21-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá [versão 2.1 atualização](storsimple-update21-release-notes.md).

