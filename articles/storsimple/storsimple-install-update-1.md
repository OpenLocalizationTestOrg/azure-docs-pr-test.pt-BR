---
title: "aaaInstall atualização 1.2 em seu dispositivo StorSimple | Microsoft Docs"
description: "Explica como tooinstall StorSimple 8000 Series atualização 1.2 em seu dispositivo da série StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 7a513923-eb77-4078-b0ab-f8e90183796a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0a7601dc0b1ce60eb854227243ecb02d6fb2c678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-12-on-your-storsimple-8000-series-device"></a>Instalar a Atualização 1.2 em seu dispositivo StorSimple série 8000
## <a name="overview"></a>Visão geral
Este tutorial explica como tooinstall atualizar 1.2 em um dispositivo StorSimple que está executando um software versão anterior tooUpdate 1. tutorial de saudação também aborda Olá são necessários outros procedimentos de atualização de saudação quando um gateway é configurado em uma interface de rede diferente de DATA 0 do dispositivo do StorSimple hello.

A atualização 1.2 inclui atualizações de software do dispositivo, as atualizações do driver LSI e atualizações de firmware de disco. Hello software e atualizações de driver LSI atualizações sem interrupções e podem ser aplicadas por meio de saudação portal clássico do Azure. atualizações de firmware de disco Olá atualizações precisam de interrupção e só podem ser aplicadas por meio da interface do Windows PowerShell saudação do dispositivo de saudação.

Dependendo de qual versão seu dispositivo está executando, você pode determinar se a atualização 1.2 será aplicada. Você pode verificar a versão do software de saudação do seu dispositivo navegando toohello **visão rápida** seção do seu dispositivo **painel**.

</br>

| Se estiver executando a versão do software... | O que acontece no portal de Olá? |
| --- | --- |
| Versão - GA |Se estiver executando a versão de lançamento (GA), não aplique essa atualização. Por favor, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) tooupdate seu dispositivo. |
| Atualização 0.1 |Portal aplica a atualização 1.2. |
| Atualização 0.2 |Portal aplica a atualização 1.2. |
| Atualização 0.3 |Portal aplica a atualização 1.2. |
| Atualização 1 |Essa atualização não estará disponível. |
| Atualização 1.1 |Essa atualização não estará disponível. |

</br>

> [!IMPORTANT]
> * Talvez você não veja 1.2 atualização imediatamente porque fazemos uma distribuição em fases de saudação atualizações. Procure novamente as atualizações em poucos dias, uma vez que elas serão disponibilizadas em breve.
> * Esta atualização inclui um conjunto de pré-verificações de manual e automática toodetermine Olá da integridade do dispositivo em termos de conectividade de rede e estado do hardware. Essas pré-verificações de são executadas somente se você aplicar atualizações de saudação do hello portal clássico do Azure.
> * É recomendável que você instalar o software de saudação e atualizações de driver via Olá portal clássico do Azure. Você só deve ficar toohello do Windows PowerShell interface de dispositivo de saudação (tooinstall atualizações) se a verificação de pré-atualização gateway de saudação falhar no portal de saudação. Olá atualizações podem levar de 5 a 10 horas tooinstall (incluindo Olá atualizações do Windows). Olá atualizações do modo de manutenção devem ser instaladas por meio de interface do Windows PowerShell de saudação do dispositivo hello. Como as atualizações do modo de manutenção são atualizações com interrupção, elas resultarão em um tempo de inatividade para seu dispositivo.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-12-via-hello-azure-classic-portal"></a>Instalar atualização 1.2 via Olá portal clássico do Azure
Executar seu dispositivo Olá seguindo as etapas tooupdate muito[atualização 1.2](storsimple-update1-release-notes.md). Use este procedimento somente se você tiver um gateway configurado na interface de rede DATA 0 no seu dispositivo.

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Verifique se o dispositivo está executando a **Atualização 1.2 do StorSimple 8000 Series (6.3.9600.17584)**. Olá **Data da última atualização** também deve ser modificado. Você verá que as atualizações do modo de manutenção estão disponíveis (essa mensagem pode continuar toobe exibido para o too24 horas após a instalação Olá atualizações).
   
   Atualizações do modo de manutenção são atualizações sem interrupção resultam em tempo de inatividade do dispositivo e só podem ser aplicadas por meio da interface do Windows PowerShell de saudação do seu dispositivo.
   
   ![Página de manutenção](./media/storsimple-install-update-1/InstallUpdate12_10M.png "Página de manutenção")
2. Baixar atualizações do modo de manutenção hello usando Olá etapas listadas na [toodownload hotfixes](#to-download-hotfixes) toosearch para e baixar KB3063416, que instala atualizações de firmware de disco (hello outras atualizações já devem estar instaladas agora).
3. Execute as etapas de saudação listadas na [instalar e verifique se os hotfixes do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall Olá atualizações do modo de manutenção.
4. Olá portal clássico do Azure no, navegue toohello **manutenção** final Olá Olá página, clique em e de página **verificar atualizações** toocheck para quaisquer atualizações do Windows e clique **instalar atualizações** . Você terminar depois que todos os de saudação atualizações são instaladas com êxito.

## <a name="install-update-12-on-a-device-that-has-a-gateway-configured-for-a-non-data-0-network-interface"></a>Instalar a Atualização 1.2 em um dispositivo com um gateway configurado em uma interface de rede diferente de DATA 0
Você deve usar este procedimento somente se você não seleção de gateway Olá durante a tentativa de atualizações de saudação tooinstall por meio de saudação portal clássico do Azure. verificação de Olá falha e você tiver um gateway atribuído tooa dados não interface de rede 0 e o dispositivo está executando um software versão anterior tooUpdate 1. Se seu dispositivo não tiver um gateway em uma interface de rede 0 sem dados, você pode atualizar seu dispositivo diretamente do hello portal clássico do Azure. Consulte [instale a atualização 1.2 via Olá portal clássico do Azure](#install-update-1.2-via-the-azure-classic-portal).

versões de software de saudação que podem ser atualizadas usando esse método são Update 0,1, atualização 0.2 e atualização 0.3.

> [!IMPORTANT]
> * Se o dispositivo está executando a versão de lançamento (GA), entre em contato com [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist com hello atualizar.
> * Toobe de necessidades esse procedimento executadas apenas uma vez tooapply 1.2 de atualização. Você pode usar as atualizações subsequentes Olá tooapply de portal clássico do Azure.
> 
> 

Se o dispositivo está executando o software de 1 de pré-atualização e tem um gateway definido para uma interface de rede diferente de DATA 0, você pode aplicar a atualização 1.2 em Olá duas maneiras a seguir:

* **Opção 1**: Baixe a atualização de saudação e aplicá-lo usando Olá `Start-HcsHotfix` cmdlet na interface do Windows PowerShell de saudação do dispositivo hello. Isso é hello recomendado de método. **Não use tooapply este método 1.2 atualização se o dispositivo está executando Update 1.0 ou 1.1 de atualização.**
* **Opção 2**: Remover configuração de gateway de saudação e hello de instalar a atualização diretamente do hello portal clássico do Azure.

Instruções detalhadas para cada um deles são fornecidas no hello seções a seguir.

## <a name="option-1-use-windows-powershell-for-storsimple-tooapply-update-12-as-a-hotfix"></a>Opção 1: Usar o Windows PowerShell para StorSimple tooapply 1.2 de atualização de hotfix
Você deve usar este procedimento somente se você estiver executando atualização 0.1, 0.2, 0.3 e se a verificação do gateway falhou durante a tentativa de atualizações de tooinstall de saudação portal clássico do Azure. Se você estiver executando o software de versão (GA), [Microsoft Support](storsimple-contact-microsoft-support.md) tooupdate seu dispositivo.

tooinstall 1.2 de atualização de hotfix, você deve baixar e instalar Olá hotfixes a seguir:

| Classificar | KB | Descrição | Tipo de atualização |
| --- | --- | --- | --- |
| 1 |KB3063418 |Atualização de software |Regular |
| 2 |KB3043005 |Atualização do controlador SAS de LSI |Regular |
| 3 |KB3063416 |Firmware de disco |Manutenção  |

Antes de usar este Olá tooapply de procedimento de atualização, verifique se:

* Ambos os controladores de dispositivo estão online.

Execute Olá etapas tooapply 1.2 de atualização a seguir. **Olá atualizações podem levar cerca de 2 horas toocomplete (aproximadamente 30 minutos para o software, 30 minutos para driver de 45 minutos para que o firmware de disco).**

[!INCLUDE [storsimple-install-update-option1](../../includes/storsimple-install-update-option1.md)]

## <a name="option-2-use-hello-azure-classic-portal-tooapply-update-12-after-removing-hello-gateway-configuration"></a>Opção 2: Usar Olá tooapply portal clássico do Azure 1.2 atualização depois de remover a configuração do gateway Olá
Este procedimento se aplica a tooStorSimple somente os dispositivos que estão executando um software versão anterior tooUpdate 1 e tem um gateway definidas em uma interface de rede diferente de dados 0. Você precisará de atualização de saudação do tooclear Olá gateway configuração tooapplying anterior.

atualização de saudação pode levar alguns toocomplete de horas. Se seus hosts estiverem em sub-redes diferentes, removendo a configuração de gateway de saudação em interfaces de iSCSI Olá pode resultar em tempo de inatividade. É recomendável que você configure o DATA 0 para o tempo de inatividade Olá tooreduce de tráfego de iSCSI.

Executar Olá interface de rede de saudação etapas toodisable com gateway Olá a seguir e aplique a atualização de saudação.

[!INCLUDE [storsimple-install-update-option2](../../includes/storsimple-install-update-option2.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá [versão 1.2 atualização](storsimple-update1-release-notes.md).

