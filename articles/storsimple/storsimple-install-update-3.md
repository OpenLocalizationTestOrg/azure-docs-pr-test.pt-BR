---
title: aaaInstall Update 3 em seu dispositivo StorSimple | Microsoft Docs
description: "Explica como tooinstall StorSimple 8000 Series atualização 3 do dispositivo da série StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c6c4634d-4f3a-4bc4-b307-a22bf18664e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a156b8919639f1c7afb0fdef3d882d40d48f1c48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-3-on-your-storsimple-8000-series-device"></a>Instalar a Atualização 3 em seu dispositivo StorSimple série 8000

## <a name="overview"></a>Visão geral

Este tutorial explica como tooinstall Update 3 em um dispositivo StorSimple executando uma versão anterior do software via Olá portal clássico do Azure e usando o método de hotfix hello. método de hotfix Hello é usado quando um gateway é configurado em uma interface de rede diferente de DATA 0 do dispositivo do StorSimple hello e você está tentando tooupdate de uma versão de software 1 pré-atualização.

A Atualização 3 inclui atualizações de software de dispositivo, firmware e driver LSI, Storport e Spaceport. Se estiver atualizando de uma versão anterior ou de atualização 2, que será também necessário tooapply iSCSI, WMI e em alguns casos, as atualizações de firmware de disco. Olá software de dispositivo, WMI, iSCSI, driver LSI, Spaceport e Storport correções atualizações sem interrupções e podem ser aplicadas por meio de saudação portal clássico do Azure. atualizações de firmware de disco Olá atualizações precisam de interrupção e só podem ser aplicadas por meio da interface do Windows PowerShell saudação do dispositivo de saudação. 

> [!IMPORTANT]
> * Um conjunto de pré-verificações de manuais e automáticas terminar instalação anterior toohello toodetermine integridade do dispositivo Olá em termos de conectividade de rede e estado do hardware. Essas pré-verificações de são executadas somente se você aplicar atualizações de saudação do hello portal clássico do Azure.
> * É recomendável que você instalar o software de saudação e atualizações de driver via Olá portal clássico do Azure. Você só deve ficar toohello do Windows PowerShell interface de dispositivo de saudação (tooinstall atualizações) se a verificação de pré-atualização gateway de saudação falhar no portal de saudação. Dependendo da versão de hello que estiver atualizando a partir, Olá atualizações podem demorar tooinstall 1.5-2,5 horas. Olá atualizações do modo de manutenção devem ser instaladas por meio de interface do Windows PowerShell de saudação do dispositivo hello. Como as atualizações do modo de manutenção são atualizações com interrupção, elas resultarão em um tempo de inatividade para seu dispositivo.
> * Se a execução hello opcional StorSimple Snapshot Manager, certifique-se de que você atualizou seu dispositivo de saudação do Gerenciador de instantâneos versão tooUpdate 2 tooupdating anterior.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-3-via-hello-azure-classic-portal"></a>Instalar a atualização 3 via Olá portal clássico do Azure
Executar seu dispositivo Olá seguindo as etapas tooupdate muito[atualização 3](storsimple-update3-release-notes.md).

> [!NOTE]
> Se você estiver aplicando a atualização 2 ou posterior (incluindo atualização 2.1), a Microsoft será capaz de toopull informações adicionais de diagnóstico de dispositivo de saudação. Como resultado, quando a nossa equipe de operações identifica dispositivos que estão tendo problemas, estamos melhores toocollect equipado informações de dispositivo de saudação e diagnosticar problemas. Aceitando a atualização 2 ou posterior, nos permite tooprovide esse suporte proativo.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

Verifique se o dispositivo está executando a **Atualização 3 do StorSimple 8000 Series (6.3.9600.17759)**. Olá **Data da última atualização** também deve ser modificado. 
   - Se você estiver atualizando de uma tooUpdate anterior da versão 2, você também verá que as atualizações do modo de manutenção de saudação estão disponíveis (essa mensagem pode continuar toobe exibido para o too24 horas após a instalação Olá atualizações).
     Atualizações do modo de manutenção são atualizações sem interrupção resultam em tempo de inatividade do dispositivo e só podem ser aplicadas por meio da interface do Windows PowerShell de saudação do seu dispositivo. Em alguns casos quando você estiver executando a atualização 1.2, o firmware de disco já pode ser atualizado, caso em que você não precisa tooinstall atualizações de qualquer modo de manutenção.
   - Se você estiver atualizando da Atualização 2 ou posterior, seu dispositivo agora deverá estar atualizado. Você poderá ignorar a próxima etapa de saudação.

Baixar atualizações do modo de manutenção hello usando Olá etapas listadas na [toodownload hotfixes](#to-download-hotfixes) toosearch para e baixar KB3121899, que instala atualizações de firmware de disco (hello outras atualizações já devem estar instaladas agora). Execute as etapas de saudação listadas na [instalar e verificar os hotfixes do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall Olá atualizações do modo de manutenção. 

## <a name="install-update-3-as-a-hotfix"></a>Instalar a Atualização 3 como um hotfix
Use este procedimento se você não seleção de gateway Olá durante a tentativa de atualizações de saudação tooinstall por meio de saudação portal clássico do Azure. verificação de Olá falha e você tiver um gateway atribuído tooa dados não interface de rede 0 e o dispositivo está executando um software versão anterior tooUpdate 1.

Olá versões de software que podem ser atualizadas usando o método de hotfix hello são:

* Atualização 0.1, 0.2, 0.3
* Atualização 1, 1.1, 1.2
* Atualização 2, 2.1, 2.2 

> [!IMPORTANT]
> * Se o dispositivo está executando a versão de lançamento (GA), entre em contato com [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist com hello atualizar.
> 
> 

método de hotfix Hello envolve Olá três etapas a seguir:

1. Baixe Olá hotfixes do hello catálogo do Microsoft Update.
2. Instalar e verificar Olá hotfixes do modo normal.
3. Instalar e verifique se o hotfix do modo de manutenção hello (somente quando a atualização de software de pré-atualização 2).

#### <a name="download-updates-for-your-device"></a>Baixar atualizações para seu dispositivo
**Se o dispositivo está executando a atualização 2.1 ou 2.2**, você deve baixar e instalar Olá hotfixes no hello prescrita ordem a seguir:

| Classificar | KB | Descrição | Tipo de atualização | Hora da instalação |
| --- | --- | --- | --- | --- |
| 1. |KB3186843 |Atualização de software &#42; |Regular  <br></br>Não interruptiva |~ 45 Min. |
| 2. |KB3186859 |Driver LSI e firmware |Regular  <br></br>Não interruptiva |~ 20 Min. |
| 3. |KB3121261 |Correção do Storport e do Spaceport  </br> Windows Server 2012 R2 |Regular  <br></br>Não interruptiva |~ 20 Min. |

&#42;  *Observe que essa atualização de software Olá consiste em dois arquivos binários: precedidos de atualização de software de dispositivo de `all-hcsmdssoftwareupdate` Olá Cis e agente do Mds precedidos de `all-cismdsagentupdatebundle`. atualização de software de dispositivo Olá deve ser instalada antes de saudação Cis e Mds agente. Também será preciso reiniciar o controlador ativo do hello via Olá `Restart-HcsController` cmdlet após a aplicação de hello Cis e atualização do agente Mds (e antes de aplicar Olá restantes atualizações).* 

**Se o dispositivo está executando a atualização 0.1, 0.2, 0.3, 1.0, 1.1, 1.2 ou 2.0**, você deve baixar e instalar Olá seguintes hotfixes no software de toohello de adição, LSI driver e firmware atualizações (Olá mostrada no anterior tabela), na Olá prescrita ordem:

| Classificar | KB | Descrição | Tipo de atualização | Hora da instalação |
| --- | --- | --- | --- | --- |
| 4. |KB3146621 |Pacote iSCSI |Regular  <br></br>Não interruptiva |~ 20 Min. |
| 5. |KB3103616 |Pacote WMI |Regular  <br></br>Não interruptiva |~ 12 Min. |

<br></br>

**Se o dispositivo está executando versões 0.2, 0.3, 1.0, 1.1 e 1.2**, talvez precise de atualizações de firmware de disco tooinstall sobre todas as atualizações de saudação mostradas no hello tabelas anteriores. Você pode verificar se você precisa Olá atualizações de firmware de disco executando Olá `Get-HcsFirmwareVersion` cmdlet. Se você estiver executando essas versões de firmware: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, em seguida, você não precisa tooinstall essas atualizações.

| Classificar | KB | Descrição | Tipo de atualização | Hora da instalação |
| --- | --- | --- | --- | --- |
| 6. |KB3121899 |Firmware de disco |Manutenção  <br></br>Interruptiva |~ 30 Min. |

<br></br>

> [!IMPORTANT]
> * Toobe de necessidades esse procedimento executadas apenas uma vez tooapply atualização 3. Você pode usar as atualizações subsequentes Olá tooapply de portal clássico do Azure.
> * Se a atualização da atualização 2.2, tempo de instalação total de saudação é fechar too1.1 horas.
> * Antes de usar este Olá tooapply de procedimento de atualização, certifique-se de que ambos os controladores de dispositivo Olá estão online e todos os componentes de hardware Olá estão íntegros.
> 
> 

Executar Olá toodownload as etapas a seguir e instalar os hotfixes hello.

[!INCLUDE [storsimple-install-update3-hotfix](../../includes/storsimple-install-update3-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá [atualização 3](storsimple-update3-release-notes.md).

