---
title: "substituição de componentes de hardware aaaStorSimple 8000 series | Microsoft Docs"
description: "Descreve como toosafely substituir PCMs hello, bateria, módulos do controlador, controladores EBOD, unidades de disco e chassi de um dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/02/2017
ms.author: alkohli
ms.custom: 
ms.openlocfilehash: 5baca8ff630a1c064cb8bf7e1024b6590f0d6b81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-hardware-component-on-your-storsimple-8000-series-device"></a>Substituir um componente de hardware no dispositivo StorSimple série 8000

## <a name="overview"></a>Visão geral
tutoriais de substituição de componente de hardware Olá descrevem os componentes de hardware de saudação do seu Microsoft Azure StorSimple 8000 series dispositivo e hello etapas necessária tooremove e substituem-los. Este artigo descreve os ícones de segurança hello, fornece ponteiros toohello detalhadas tutoriais e listas Olá componentes que podem ser trocadas.

> [!IMPORTANT]
> Antes de tentar tooremove ou substituir qualquer componente do StorSimple, certifique-se de que você examine Olá [convenções de ícone de segurança](#safety-icon-conventions) e outros [precauções de segurança](storsimple-safety.md).


### <a name="safety-icon-conventions"></a>Convenções de ícones de segurança
Olá tabela a seguir descreve os ícones de segurança Olá usados nos tutoriais. Preste atenção ícones de segurança toothese como percorrer Olá etapas tooremove e substitua os componentes do dispositivo.

| ícone | Texto | Informações adicionais |
|:--- |:--- |:--- |
| ![Ícone de aviso](./media/storsimple-hardware-component-replacement/Warning.png) |**PERIGO!** |Indica uma situação perigosa que, se não for evitada, resultará em morte ou lesões graves. Esta palavra é situações mais extremas toohello limitado. |
| ![Ícone de aviso](./media/storsimple-hardware-component-replacement/Warning.png) |**AVISO!** |Indica uma situação perigosa que, se não for evitada, pode causar lesões graves ou de morte. |
| ![Ícone de cuidado](./media/storsimple-hardware-component-replacement/Caution.png) |**CUIDADO!** |Indica uma situação perigosa que, se não for evitada, pode em uma lesão pequena ou moderada. |
| ![Ícone de observação](./media/storsimple-hardware-component-replacement/NoticeIcon.png) |**OBSERVAÇÃO:** |Indica informações consideradas importantes, mas não são relacionadas a riscos. |
| ![Ícone de choque elétrico](./media/storsimple-hardware-component-replacement/Electric.png) |**Risco de choque elétrico** |Indica alta tensão. |
| ![ícone de peso pesado](./media/storsimple-hardware-component-replacement/Weight.png) |**Peso pesado** | |
| ![Ícone de nenhuma peça operada pelo usuário](./media/storsimple-hardware-component-replacement/NoUserServiceableParts.png) |**Nenhuma peça é operada pelo usuário** |Não acesse a menos que seja devidamente treinado. |
| ![Ícone de leia as instruções](./media/storsimple-hardware-component-replacement/ReadInstructions.png) |**Leia todas as instruções primeiro** | |
| ![Ícone de risco de tombamento](./media/storsimple-hardware-component-replacement/TipHazard.png) |**Risco de tombamento** | |

### <a name="before-you-begin"></a>Antes de começar
Familiarize-se com as informações de segurança Olá sobre os ícones de dispositivo e de segurança usados neste tutorial. Vá muito[com segurança instalar e operar o seu dispositivo StorSimple](storsimple-safety.md) para obter informações completas. Ser Olá-se de tooreview [precauções de segurança](storsimple-safety.md#handling-precautions) antes de manipular seu dispositivo StorSimple.

Antes de tentar tooreplace um componente, considere Olá informações a seguir.

![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Electrical Shock Icon](./media/storsimple-hardware-component-replacement/Electric.png) **AVISO!**

* Proteja-se corretamente usando um tapete antiestático ao lidar com módulos e componentes do seu dispositivo StorSimple.
* Não toque em nenhum circuito. Use guias e alavancas Olá fornecida ao manusear componentes que podem ter circuitos expostos.

![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Notice Icon](./media/storsimple-hardware-component-replacement/NoticeIcon.png) **OBSERVAÇÃO:**

Quando você substituir um módulo, **nunca deixe nenhuma seção vazia na parte posterior de saudação do compartimento de saudação**. Obter uma substituição ou um módulo em branco antes de remover a peça com problema hello.

## <a name="hardware-component-replacement-procedures"></a>Procedimentos de substituição de componentes de hardware
O dispositivo da série StorSimple 8000 consiste em vários módulos de plug-in no hello principal e/ou compartimentos EBOD. Olá 8100 tem um único compartimento primário, enquanto Olá 8600 é um dispositivo de compartimento duplo com um compartimento principal e um compartimento EBOD.

Olá principais componentes de hardware em seu dispositivo estão resumidos na Olá tabelas a seguir. Clique em link Olá Olá **procedimento de substituição** coluna toogo toohello associado tutorial.

| Componentes | Quantidade presente | Módulo plug-in? | Procedimento de substituição |
|:--- |:--- |:--- |:--- |
| Chassi |1 |Não |[Substitua o chassi Olá em seu dispositivo StorSimple](storsimple-8000-chassis-replacement.md) |
| Controladores principais |2 |Sim |[Substituir um módulo de controlador em seu dispositivo StorSimple](storsimple-8000-controller-replacement.md) |
| Módulos de energia e resfriamento (PCMs) de 764W |2 |Sim |[Substituir um módulo de energia e resfriamento em seu dispositivo StorSimple](storsimple-8000-power-cooling-module-replacement.md) |
| Bateria de backup |2 |Sim |[Substituir o módulo de bateria de backup Olá em seu dispositivo StorSimple](storsimple-8000-battery-replacement.md) |
| Unidades de disco |12 |Sim |[Substituir uma unidade de disco em seu dispositivo StorSimple](storsimple-8000-disk-drive-replacement.md) |

**Tabela 1** componentes de Hardware no compartimento primário Olá

compartimento principal Hello e compartimento do EBOD Olá diferem nos seus módulos de e/s. Além disso, PCMs Olá têm diferentes voltagens. Olá PCMs no compartimento primário Olá 764 W, enquanto que aqueles no compartimento EBOD de saudação são 580 w. PCMs Olá no hello primário compartimento também contêm um módulo de bateria de backup.

| Componentes | Quantidade presente | Módulo plug-in? | Procedimento de substituição |
|:--- |:--- |:--- |:--- |
| Chassi |1 |Não |[Substitua o chassi Olá em seu dispositivo StorSimple](storsimple-8000-chassis-replacement.md) |
| Controladores do EBOD |2 |Sim |[Substituir um controlador EBOD em seu dispositivo StorSimple](storsimple-8000-ebod-controller-replacement.md) |
| Módulos de energia e resfriamento (PCMs) de 580W |2 |Sim |[Substituir um módulo de energia e resfriamento em seu dispositivo StorSimple](storsimple-8000-power-cooling-module-replacement.md) |
| Unidades de disco |12 |Sim |[Substituir uma unidade de disco em seu dispositivo StorSimple](storsimple-8000-disk-drive-replacement.md) |

**Tabela 2** componentes de Hardware no compartimento EBOD de saudação

módulos de plug-in de saudação no dispositivo Olá são realçados em Olá frontal e traseiros diagramas a seguir. Você pode usar esses local de saudação toodetermine diagramas de saudação vários módulos de plug-in se for necessária uma substituição. diagrama da parte frontal Olá mostra Olá unidades de disco e diagramas da saudação EBOD parte traseira Olá compartimento e o compartimento principal Olá mostram Olá módulos de plug-in.

![Frontplane do dispositivo com unidades de disco](./media/storsimple-hardware-component-replacement/IC741028.png)

**Figura 1** frontal do dispositivo Olá

| Rótulo | Descrição |
|:--- |:--- |
| 0 - 11 |Unidades de disco (total de 12) |

Compartimento principal hello e compartimento do EBOD Olá têm módulos de portador da unidade. chassi Olá abriga doze 3.5" unidades de disco organizadas em um formato de 3 a 4.

![Backplane dos módulos do compartimento primário do dispositivo](./media/storsimple-hardware-component-replacement/IC740994.png)

**Figura 2** parte traseira do compartimento principal Olá

| Rótulo | Descrição |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |Controlador 0 |
| 4 |Controlador 1 |

![Backplane dos módulos plug-in do compartimento EBOD do dispositivo](./media/storsimple-hardware-component-replacement/IC769599.png)

**Figura 3** parte traseira do compartimento EBOD de saudação

| Rótulo | Descrição |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |Controlador 0 do EBOD |
| 4 |Controlador 1 do EBOD |

## <a name="field-replaceable-units"></a>Unidades renováveis
Olá unidades substituíveis de campo (FRUs) a seguir está disponível para seu dispositivo StorSimple:

* Chassi (incluindo o painel de operações integradas Olá)
* PCM de CA de 764 W
* PCM de CA de 580 W
* Unidade de disco rígido com módulo de suporte de unidade
* Módulo de controlador
* Módulo de controlador do EBOD
* Módulo de bateria de backup
* Kit do trilho de montagem em rack

Por favor, [entre em contato com o Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder qualquer uma dessas unidades de substituição.

## <a name="next-steps"></a>Próximas etapas
Examinar todos os [as informações de segurança](storsimple-safety.md) antes de tentar tooreplace um componente de hardware do StorSimple.

