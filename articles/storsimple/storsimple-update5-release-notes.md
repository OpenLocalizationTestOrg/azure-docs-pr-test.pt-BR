---
title: "Notas de versão do aaaStorSimple 8000 Series atualização 5 | Microsoft Docs"
description: "Descreve os novos recursos do hello, problemas e soluções alternativas para StorSimple 8000 Series atualização 5."
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
ms.date: 08/23/2017
ms.author: alkohli
ms.openlocfilehash: 9eb8ffb97b41ce3d4f1ffdf2975f904d0a2958e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-5-release-notes"></a>Notas de versão da Atualização 5 para o StorSimple Série 8000

## <a name="overview"></a>Visão geral

Olá notas de versão a seguir descrevem Olá novos recursos e identificam os problemas abertos críticos Olá para StorSimple 8000 Series atualização 5. Eles também contêm uma lista de atualizações de software do hello StorSimple incluídas nesta versão.

Atualização 5 pode ser aplicado tooany o dispositivo StorSimple executar Update 0,1 a atualização 4. versão do dispositivo Olá associado com a atualização 5 é 6.3.9600.17845.

Examine as informações de saudação contidas na versão Olá notas antes de implantar Olá atualizar em sua solução StorSimple.

> [!IMPORTANT]
> * A Atualização 5 tem o software do dispositivo, o firmware do disco, a segurança do SO bem como outras atualizações do sistema operacional. Demora cerca de 4 horas tooinstall essa atualização. A atualização de firmware de disco é uma atualização com tempo de inatividade e resulta em um tempo de inatividade para o dispositivo. É recomendável que você aplique a atualização 5 tookeep seu dispositivo atualizado.
> * Para novas versões, você poderá não ver atualizações imediatamente porque fazemos uma distribuição em fases de saudação atualizações. Aguarde alguns dias e procure atualizações novamente, pois elas serão disponibilizadas em breve.

## <a name="whats-new-in-update-5"></a>Novidades na Atualização 5

Olá seguintes principais melhorias e correções de bugs foram feitas em 5 de atualização.

* **Uso do Azure Active Directory (AAD) tooauthenticate com o serviço do Gerenciador de dispositivos de StorSimple** – de atualização 5 em diante, o Active Directory do Azure é tooauthenticate usado com o serviço do Gerenciador de dispositivos de StorSimple hello. mecanismo de autenticação Olá antigo será substituído até dezembro de 2017. Todos os usuários de saudação devem incluir Olá novas URLs de autenticação em suas regras de firewall. Para obter mais informações, vá muito[URLs de autenticação listadas no hello requisitos de rede para seu dispositivo StorSimple](storsimple-8000-system-requirements.md#url-patterns-for-azure-portal).

    Se a URL de saudação de autenticação não está incluído nas regras de firewall Olá, usuários Olá verá um alerta crítico que seu dispositivo StorSimple não pôde autenticar com o serviço de saudação. Se usuários Olá veem esse alerta, ele deverá tooinclude Olá nova URL de autenticação. Para obter mais informações, vá muito[StorSimple rede alertas](storsimple-8000-manage-alerts.md#networking-alerts).

* **Nova versão do StorSimple Snapshot Manager** – uma nova versão do StorSimple Snapshot Manager foi liberada com a Atualização 5. É recomendável que você atualize a versão toothis. Esta versão é compatível com todos os dispositivos de StorSimple Olá que estão executando a atualização 3 ou posterior. Para obter mais informações, vá muito[implantar o Gerenciador de instantâneos StorSimple](storsimple-snapshot-manager-deployment.md).


## <a name="issues-fixed-in-update-5"></a>Problemas corrigidos na Atualização 5

Olá tabela a seguir fornece um resumo dos problemas que foram corrigidos na atualização 5.

| Não | Recurso | Problema | Aplica-se o dispositivo toophysical | Aplica-se o dispositivo toovirtual |
| --- | --- | --- | --- | --- |
| 1 |Comunicação remota do Windows PowerShell |Na versão anterior do hello, um usuário deve receber um erro durante a tentativa de tooestablish toohello uma conexão remota StorSimple Appliance de nuvem por meio do Windows PowerShell. Esse problema foi causado pela raiz e corrigido nesta versão. |Não |Sim |
| 2 |Modelos de largura de banda |Na versão anterior, havia um problema com os modelos de largura de banda que resultou em menos largura de banda que o dispositivo Olá foi configurado para. Esse problema foi corrigido nesta versão. |Sim |Sim |
| 3 |Failover |Na versão anterior, quando um dispositivo com um grande número de volumes falhou tooanother dispositivo executando o Update 4, processo Olá falhará durante a tentativa de registros de controle de acesso tooapply hello. Esse problema foi corrigido nesta versão. |Sim |Sim |



## <a name="known-issues-in-update-5-from-previous-releases"></a>Problemas de versões anteriores conhecidos na Atualização 5

Não há nenhum novo problema conhecido na Atualização 5. Para obter uma lista dos problemas transportadas tooUpdate 5 de versões anteriores, ir muito[notas de versão da atualização 3](storsimple-update3-release-notes.md#known-issues-in-update-3).

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-5"></a>Controlador SAS (SCSI anexado em série) e atualizações de firmware na Atualização 5

Esta versão tem controlador SAS e atualizações de firmware e driver LSI. Para obter mais informações sobre como tooinstall essas atualizações, consulte [instalar atualização 5](storsimple-8000-install-update-5.md) em seu dispositivo StorSimple.

## <a name="storsimple-cloud-appliance-updates-in-update-5"></a>Atualizações do Dispositivo de Nuvem StorSimple na Atualização 5

Esta atualização não pode ser aplicado toohello StorSimple Appliance de nuvem (também conhecido como dispositivo virtual Olá). Novos dispositivos de nuvem necessário toobe criado usando a imagem de saudação atualização 5. Para obter informações sobre como toocreate um dispositivo StorSimple de nuvem, ir muito[implantar e gerenciar um dispositivo de nuvem StorSimple](storsimple-8000-cloud-appliance-u2.md).

## <a name="next-step"></a>Próxima etapa

Saiba como muito[instalar atualização 5](storsimple-8000-install-update-5.md) em seu dispositivo StorSimple.

