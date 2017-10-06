---
title: aaaReplace uma unidade de disco em um dispositivo StorSimple | Microsoft Docs
description: Explica como tooreplace um disco da unidade em um compartimento principal do StorSimple ou um compartimento EBOD.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 98890d36-b613-40fd-994e-330dd907a8a1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d2c78a6d951b0f00ac42e74a34cf1bc83952a3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a>Substituir uma unidade de disco em seu dispositivo StorSimple
## <a name="overview"></a>Visão geral
Este tutorial explica como remover e substituir uma unidade de disco rígido com defeito ou com falha em um dispositivo Microsoft Azure StorSimple. tooreplace uma unidade de disco, você precisa:

* Solte o bloqueio inviolável Olá
* Remova a unidade de disco de saudação
* Instalar a unidade de disco de substituição Olá

> [!IMPORTANT]
> Antes de remover e substituir uma unidade de disco, revise as informações de segurança de saudação em [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="disengage-hello-antitamper-lock"></a>Solte o bloqueio inviolável Olá
Este procedimento explica como os bloqueios invioláveis de saudação em seu dispositivo StorSimple podem ser encaixados ou desencaixados ao substituir Olá unidades de disco. bloqueios invioláveis Olá são encaixados nas alças da portadora unidade hello e eles são acessados por meio de uma pequena abertura na seção de trava de saudação do identificador de saudação. As unidades são fornecidas com hello bloqueios conjunto toohello bloqueado posição.

#### <a name="toounlock-hello-antitamper-lock"></a>bloqueio inviolável do toounlock Olá
1. Insira cuidadosamente a chave de bloqueio de saudação (uma fenda T10 "inviolável" que a Microsoft forneceu) na abertura de saudação na alça de saudação e no soquete. 
   
   > [!NOTE]
   > Se ativar o bloqueio inviolável hello, indicador Olá vermelho estará visível na abertura de saudação.
   > 
   > 
   
    ![Unidade de disco bloqueada](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    **Figura 1** Bloqueio antiviolação ativado
   
   | Rótulo | Descrição |
   |:--- |:--- |
   | 1 |Abertura do indicador |
   | 2 |Bloqueio antiviolação |
2. Rotação da chave de saudação no sentido anti-horário até que o indicador vermelho de saudação não estiver visível na abertura de saudação acima chave hello.
3. Remova a chave de saudação.
   
    ![Unidade de disco desbloqueada](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    **Figura 2** Unidade de disco desbloqueada
4. unidade de disco Olá agora podem ser removida.

Siga as etapas de saudação no bloqueio de saudação tooengage inversa.

## <a name="remove-hello-disk-drive"></a>Remova a unidade de disco de saudação
O dispositivo StorSimple dá suporte a uma configuração de espaços de armazenamento similar a RAID 10. Isso significa que ele pode operar normalmente com um disco com falha, unidade de estado sólido (SSD) ou unidade de disco rígido (HD). 

> [!IMPORTANT]
> * Se o sistema tiver mais de um disco com falha, não remova mais de um SSD ou HDD do sistema hello em qualquer ponto no tempo. Isso pode resultar em perda de dados.
> * Lembre-se de colocar um SSD de reposição em um slot que continha anteriormente um SSD. Da mesma forma, coloque um HDD de reposição em um slot que continha anteriormente um HDD.
> * Em Olá portal clássico do Azure, as entradas são numeradas de 0 a 11. Portanto, se o portal de saudação mostra que um disco no slot 2 falhou, no dispositivo Olá, procure Olá o disco com falha no terceiro slot de saudação do hello superior esquerdo.
> 
> 

Unidades podem ser removidas e substituídas enquanto o sistema hello está funcionando.

#### <a name="tooremove-a-drive"></a>tooremove uma unidade
1. tooidentify Olá disco com falha, no hello portal clássico do Azure, vá muito**dispositivos** > **manutenção** > **Status do Hardware**. Como um disco pode falhar no compartimento primário hello e/ou em um compartimento EBOD (se você estiver usando um modelo 8600), examinar status Olá de discos de saudação em **componentes compartilhados** e, em **EBOD componentes compartilhados do compartimento**. Um disco com falha em um compartimento será mostrado com  status vermelho.
2. Localize Olá unidades na frente de saudação do compartimento principal hello ou compartimento do EBOD hello. 
3. Se o disco Olá estiver desbloqueado, continue toohello próxima etapa. Se Olá disco estiver bloqueado, desbloqueá-lo seguindo o procedimento Olá [desencaixar o bloqueio inviolável Olá](#disengage-the-antitamper-lock).
4. Pressione Olá preto trava no módulo Olá de portador de unidade e puxe a alça do portador da unidade Olá para fora da frente de saudação do chassi de saudação. 
   
    ![Liberando a alça da unidade de disco](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    **Figura 3** liberando identificador de unidade de saudação
5. Quando a alça do portador da unidade Olá estiver totalmente expandida, deslize o portador da unidade de saudação fora do chassi de saudação. 
   
    ![Deslizando o disco para fora da unidade de disco](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    **Figura 4** deslizante Olá a unidade de disco fora da portadora Olá

## <a name="install-hello-replacement-disk-drive"></a>Instalar a unidade de disco de substituição Olá
Depois de uma unidade falhou no seu dispositivo StorSimple e removê-lo, siga este procedimento tooreplace com uma nova unidade.

#### <a name="tooinsert-a-drive"></a>tooinsert uma unidade
1. Verifique a alça do portador da unidade hello está totalmente estendida, conforme mostrado no Olá a imagem a seguir.
   
    ![Unidade de disco com alça estendida](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    **Figura 5** Unidade com alça estendida
2. Deslize o portador da unidade de saudação todo caminho de saudação no chassi hello. 
   
    ![Deslizando o disco para dentro do suporte da unidade de disco](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    **Figura 6** portador da unidade de saudação deslizante no chassi Olá
3. Com hello unidade operadora Olá inserido, feche unidade operadora identificador ao continuando toopush Olá portador da unidade no chassi hello, até que a alça do portador da unidade Olá chegue à posição bloqueada.
4. Use Olá chave de bloqueio fornecida pela alça do portador da Microsoft (de fenda Torx inviolável) toosecure Olá no lugar ativando o parafuso de bloqueio Olá um quarto de volta no sentido horário.
5. Verifique se Olá substituição foi bem-sucedida e unidade hello está operacional acessando Olá portal clássico do Azure e navegando muito**manutenção** > **Status do Hardware**. Em **componentes compartilhados** ou **componentes compartilhados do compartimento do EBOD**, status da unidade Olá deve estar verde, indicando que ele esteja íntegro.
   
   > [!NOTE]
   > Ele pode levar algumas horas para Olá disco status tooturn verde após a substituição de saudação.
   > 
   > 

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).

