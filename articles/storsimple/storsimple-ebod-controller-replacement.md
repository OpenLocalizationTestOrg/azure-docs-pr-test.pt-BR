---
title: aaaReplace um controlador EBOD StorSimple | Microsoft Docs
description: Explica como tooremove e substituir um ou ambos os controladores EBOD em um dispositivo 8600 StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5d29de2ee30bfdd70910050eee5cfa1d293d444f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a>Substituir um controlador EBOD em seu dispositivo StorSimple
## <a name="overview"></a>Visão geral
Este tutorial explica como tooreplace um módulo do controlador EBOD com falha em seu dispositivo StorSimple do Microsoft Azure. tooreplace um módulo do controlador EBOD, você precisa:

* Remover o controlador EBOD com falha de saudação
* Instalar um novo controlador EBOD

Considere Olá informações a seguir antes de começar:

* Módulos EBOD em branco precisam ser inseridos em todos os slots não utilizados. compartimento de saudação não será resfriado corretamente se um slot for deixado aberto.
* controlador do EBOD Olá é intercambiável e pode ser removido ou substituído. Não remova um módulo com falha até que você tenha uma peça de reposição. Quando você iniciar o processo de substituição hello, você deve finalizá-lo dentro de 10 minutos.

> [!IMPORTANT]
> Antes de tentar tooremove ou substituir qualquer componente do StorSimple, certifique-se de que você examine Olá [convenções de ícone de segurança](storsimple-safety.md#safety-icon-conventions) e outros [precauções de segurança](storsimple-safety.md).
> 
> 

## <a name="remove-an-ebod-controller"></a>Remover um controlador EBOD
Antes de falha ao substituir Olá módulo controlador EBOD em seu dispositivo StorSimple, verifique se esse Olá outro módulo controlador EBOD está ativo e em execução. Olá procedimento e a tabela a seguir explicam como tooremove Olá módulo do controlador EBOD.

#### <a name="tooremove-an-ebod-module"></a>tooremove um módulo EBOD
1. Olá Abrir portal clássico do Azure.
2. Navegue muito**dispositivos** > **manutenção** > **Status do Hardware**e verifique se o LED de status Olá Olá para Olá EBOD ativo módulo do controlador é verde e hello LED para o módulo do controlador EBOD Olá falhado é vermelha.
3. Localize o módulo do controlador EBOD Olá falhado no hello parte posterior do dispositivo hello.
4. Remova os cabos de saudação que se conectam a saudação EBOD módulo toohello controlador antes de retirar o módulo EBOD de saudação do sistema hello.
5. Tome nota da porta SAS exata de saudação do módulo do controlador EBOD Olá que estava conectado toohello controlador. Configuração de toothis toorestore necessário Olá sistema será depois de substituir o módulo EBOD de saudação. 
   
   > [!NOTE]
   > Normalmente, isso será a porta A, que é rotulada como **hospedar em** em Olá diagrama a seguir.
   > 
   > 
   
    ![Backplane do controlador EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     **Figura 1** Parte posterior do módulo EBOD
   
   | Rótulo | Descrição |
   |:--- |:--- |
   | 1 |LED de falha |
   | 2 |LED de energia |
   | 3 |Conectores SAS |
   | 4 |LEDs de SAS |
   | 5 |Portas seriais apenas para uso em fábrica |
   | 6 |Porta A (Host in) |
   | 7 |Porta B (Host out) |
   | 8 |Porta C (Apenas para uso em fábrica) |

## <a name="install-a-new-ebod-controller"></a>Instalar um novo controlador EBOD
Olá procedimento e a tabela a seguir explicam como tooinstall um módulo do controlador EBOD no seu dispositivo StorSimple.

#### <a name="tooinstall-an-ebod-controller"></a>tooinstall um controlador EBOD
1. Verifique o dispositivo EBOD de saudação danos, especialmente toohello conector da interface. Não instale o novo controlador de EBOD Olá se algum pino estiver torto.
2. Com travas Olá Olá abra posição, módulo de saudação do slide para compartimento Olá até Olá travas.
   
    ![Instalando o controlador EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    **Figura 2** módulo do controlador do EBOD instalando Olá
3. Trava Olá fechar. Você ouvirá um clique quando Olá trava estiver no lugar.
   
    ![Liberando a trava do EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    **Figura 3** fechando a trava do módulo EBOD Olá
4. Reconecte os cabos de saudação. Use Olá configuração exata que foi apresentada antes da substituição de saudação. Consulte o diagrama a seguir de saudação e de tabela para obter detalhes sobre como os cabos de saudação do tooconnect.
   
    ![Cabeamento do dispositivo 4U para alimentação](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    **Figura 4**. Reconectando os cabos
   
   | Rótulo | Descrição |
   |:--- |:--- |
   | 1 |Compartimento principal |
   | 2 |PCM 0 |
   | 3 |PCM 1 |
   | 4 |Controlador 0 |
   | 5 |Controlador 1 |
   | 6 |Controlador 0 do EBOD |
   | 7 |Controlador 1 do EBOD |
   | 8 |Compartimento EBOD |
   | 9 |Unidades de distribuição de energia |

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).

