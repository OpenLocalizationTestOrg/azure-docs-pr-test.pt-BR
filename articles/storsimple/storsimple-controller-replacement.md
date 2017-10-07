---
title: aaaReplace um controlador do dispositivo StorSimple | Microsoft Docs
description: "Explica como tooremove e substituir um ou ambos os módulos do controlador em seu dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e25b52b7-60f5-47f3-bffc-6c157d57ab5d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/03/2017
ms.author: alkohli
ms.openlocfilehash: ebf5c5830120857f69909113e3a111f4dda30e57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-controller-module-on-your-storsimple-device"></a>Substituir um módulo de controlador em seu dispositivo StorSimple
## <a name="overview"></a>Visão geral
Este tutorial explica como tooremove e substituir um ou ambos os módulos do controlador em um dispositivo StorSimple. Ele também discute Olá subjacente lógica para cenários de substituição de controlador único e duplo hello.

> [!NOTE]
> Tooperforming anterior a substituição do controlador, é recomendável que você sempre atualize sua versão mais recente do firmware toohello de controlador.
> 
> tooprevent danificar o dispositivo StorSimple tooyour, não ejete o controlador de saudação até Olá LEDs estão sendo exibidos como um dos seguintes hello:
> 
> * Todas as luzes estão desligadas.
> * LED 3, ![ícone de marca de seleção verde](./media/storsimple-controller-replacement/HCS_GreenCheckIcon.png) e ![ícone de cruz vermelha](./media/storsimple-controller-replacement/HCS_RedCrossIcon.png) estão piscando e LED 0 e LED 7 estão **ACESOS**.
> 
> 

Olá, a tabela a seguir mostra Olá suporte para cenários de substituição de controlador.

| Caixa | Cenário de substituição | Procedimento aplicável |
|:--- |:--- |:--- |
| 1 |Um controlador está em um estado de falha, hello outro controlador está funcionando e ativo. |[Única substituição do controlador](#replace-a-single-controller), que descreve Olá [lógica por trás de uma substituição de controlador único](#single-controller-replacement-logic), bem como Olá [etapas de substituição](#single-controller-replacement-steps). |
| 2 |Ambos os controladores Olá falharam e precisam ser substituídos. chassi Hello, discos e compartimento de disco estão funcionando. |[Substituição de controlador duplo](#replace-both-controllers), que descreve Olá [lógica por trás de uma substituição de controlador duplo](#dual-controller-replacement-logic), bem como Olá [etapas de substituição](#dual-controller-replacement-steps). |
| 3 |Controladores de Olá mesmo dispositivo ou de diferentes dispositivos estão trocados. chassi Hello, discos e compartimentos de disco estão funcionando. |Será exibida uma mensagem de alerta de incompatibilidade do slot. |
| 4 |Um controlador está ausente e Olá outro controlador falhar. |[Substituição de controlador duplo](#replace-both-controllers), que descreve Olá [lógica por trás de uma substituição de controlador duplo](#dual-controller-replacement-logic), bem como Olá [etapas de substituição](#dual-controller-replacement-steps). |
| 5 |Um ou ambos os controladores falharam. Você não pode acessar o dispositivo Olá por meio do console serial hello ou a comunicação remota do Windows PowerShell. |[Contate o Suporte da Microsoft](storsimple-contact-microsoft-support.md) para saber o procedimento manual de substituição do controlador. |
| 6 |controladores de saudação tem uma versão de compilação diferente, que pode ser devido a:<ul><li>Os controladores têm uma versão de software diferente.</li><li>Os controladores têm uma versão de firmware diferente.</li></ul> |Se as versões de software do controlador de saudação forem diferentes, lógica de substituição de saudação detecta que e Olá de atualizações de versão do software no controlador de substituição de saudação.<br><br>Se versões de firmware do controlador de saudação são diferentes e Olá antiga versão de firmware **não** automaticamente atualizável, uma mensagem de alerta será exibido no hello portal clássico do Azure. Você deve verificar se há atualizações e instalar atualizações de firmware de saudação.</br></br>Se versões de firmware do controlador de saudação são diferentes e a antiga versão de firmware Olá pode ser atualizado automaticamente, lógica de substituição de controlador Olá detectará isso e depois Olá controlador for iniciado, firmware Olá será atualizado automaticamente. |

É necessário tooremove um módulo do controlador que tenha falhado. Um ou ambos os módulos do controlador Olá podem falhar, o que pode resultar em uma substituição de controlador único ou substituição de controlador duplo. Para procedimentos de substituição e Olá lógica-los, consulte o seguinte hello:

* [Substituir controlador único](#replace-a-single-controller)
* [Substituir ambos os controladores](#replace-both-controllers)
* [Remover um controlador](#remove-a-controller)
* [Inserir um controlador](#insert-a-controller)
* [Identificar controlador ativo de saudação do dispositivo](#identify-the-active-controller-on-your-device)

> [!IMPORTANT]
> Antes de remover e substituir um controlador, revise as informações de segurança de Olá em [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="replace-a-single-controller"></a>Substituir controlador único
Quando um dos Olá dois controladores no dispositivo do Microsoft Azure StorSimple Olá falhou, está funcionando corretamente ou está ausente, será necessário tooreplace um único controlador. 

### <a name="single-controller-replacement-logic"></a>Lógica de substituição de controlador único
Em uma substituição de controlador único, você deve primeiro remover o controlador com falha hello. (Olá restante no dispositivo de saudação é Olá active controlador.) Quando você insere o controlador de substituição hello, hello ações a seguir ocorrem:

1. controlador de substituição de saudação imediatamente começa a se comunicar com o dispositivo StorSimple hello.
2. Um instantâneo de saudação virtual VHD (disco rígido) para o controlador ativo Olá é copiado no controlador de substituição de saudação.
3. instantâneo de saudação é modificado para que quando o controlador de saudação de substituição inicia nesse VHD, ele será reconhecido como um controlador em espera.
4. Quando Olá modificações forem concluídas, o controlador de substituição Olá será iniciado como controlador em espera hello.
5. Quando ambos os controladores Olá estão em execução, o cluster Olá fica online.

### <a name="single-controller-replacement-steps"></a>Etapas de substituição de controlador único
Concluir Olá etapas a seguir se um dos controladores de saudação no seu dispositivo do Microsoft Azure StorSimple falhar. (hello outro controlador deve estar ativo e em execução. Se ambos os controladores falharem ou mau funcionamento, vá muito[etapas de substituição de controlador duplo](#dual-controller-replacement-steps).)

> [!NOTE]
> Pode levar de 30 a 45 minutos para Olá controlador toorestart e recuperar completamente do procedimento de substituição de controlador único hello. tempo total de saudação para todo o procedimento hello, incluindo a conexão Olá cabos, é de aproximadamente 2 horas.
> 
> 

#### <a name="tooremove-a-single-failed-controller-module"></a>tooremove um módulo do controlador com falha único
1. No hello portal clássico do Azure, acesse o serviço StorSimple Manager toohello, clique em Olá **dispositivos** guia e, em seguida, clique em Olá nome da saudação dispositivo que você deseja toomonitor.
2. Vá muito**manutenção > Status do Hardware**. status de saudação do controlador 0 ou controlador 1 deve ser vermelho, que indica uma falha.
   
   > [!NOTE]
   > saudação de controlador com falha na substituição de um único controlador é sempre um controlador em espera.
   > 
   > 
3. Use a Figura 1 e hello módulo do controlador com falha de saudação de toolocate de tabela a seguir.  
   
    ![Backplane dos módulos do compartimento primário do dispositivo](./media/storsimple-controller-replacement/IC740994.png)
   
    **Figura 1** Parte posterior do dispositivo StorSimple
   
   | Rótulo | Descrição |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Controlador 0 |
   | 4 |Controlador 1 |
4. No controlador com falha do hello, remova todos os cabos de rede Olá conectado Olá das portas de dados. Se você estiver usando um modelo 8600, remova também Olá que cabos de SAS que se conectam Olá toohello EBOD controlador.
5. Siga as etapas de saudação em [remover um controlador](#remove-a-controller) tooremove Olá falha no controlador. 
6. Substituição de fábrica Olá instalar em Olá mesmo slot do qual controlador com falha Olá foi removida. Isso dispara a lógica de substituição de controlador único hello. Para saber mais, consulte [Lógica de substituição do controlador único](#single-controller-replacement-logic).
7. Enquanto a lógica de substituição de controlador único Olá progride no plano de fundo hello, reconecte os cabos de saudação. Tomar cuidado tooconnect que todos os cabos de Olá Olá exatamente mesma maneira que estavam conectados antes da substituição de saudação.
8. Depois Olá controlador reiniciar, verifique Olá **status do controlador** e hello **Cluster status** no hello Azure tooverify portal clássico que Olá controlador estará em estado íntegro tooa voltar e está em modo de espera .

> [!NOTE]
> Se você estiver monitorando dispositivo Olá por meio do console serial hello, você poderá ver várias reinicializações enquanto o controlador hello está se recuperando do procedimento de substituição de saudação. Quando o menu do console serial Olá é apresentado, você sabe que Olá substituição foi concluída. Se Olá menu não apareça dentro de duas horas do início da substituição do controlador hello, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md).
>
> Iniciando atualização 4, você também pode usar o cmdlet de saudação `Get-HCSControllerReplacementStatus` na interface do Windows PowerShell Olá Olá status do dispositivo toomonitor saudação do processo de substituição de controlador hello.
> 

## <a name="replace-both-controllers"></a>Substituir ambos os controladores
Quando ambos os controladores de dispositivo do Microsoft Azure StorSimple Olá falharam, estão funcionando corretamente ou estão ausente, será necessário tooreplace ambos os controladores. 

### <a name="dual-controller-replacement-logic"></a>Lógica de substituição do controlador duplo
Na substituição de um controlador duplo, primeiro remova os dois controladores com falha e insira as peças de reposição. Quando os dois controladores de substituição Olá são inseridos, hello ações a seguir ocorrem:

1. controlador de substituição Olá no slot 0 verifica a seguir hello:
   
   1. Ele está usando versões atuais do hello firmware e software?
   2. É uma parte do cluster Olá?
   3. É o controlador de par de saudação em execução e está em cluster?
      
      Se nenhuma dessas condições for verdadeira, o controlador de saudação olha para backup diário mais recente de saudação (localizado em Olá **nonDOMstorage** na unidade S). Olá controlador cópias Olá instantâneo mais recente da saudação VHD de backup hello.
2. controlador Olá no slot 0 usa Olá instantâneo tooimage em si.
3. Enquanto isso, controlador Olá no slot 1 aguarda para geração de imagens do controlador 0 toocomplete hello e iniciar.
4. Depois que o controlador 0 for iniciado, o controlador 1 detecta cluster de saudação criado pelo controlador 0, que aciona a lógica de substituição de controlador único hello. Para saber mais, consulte [Lógica de substituição do controlador único](#single-controller-replacement-logic).
5. Posteriormente, ambos os controladores estarão funcionando e Olá cluster ficará online.

> [!IMPORTANT]
> Após uma substituição de controlador duplo, depois que o dispositivo StorSimple Olá estiver configurado, é essencial que você tire um manual de backup do dispositivo hello. Os backups diários da configuração do dispositivo não são acionados antes de 24 horas. Trabalhar com [Microsoft Support](storsimple-contact-microsoft-support.md) toomake um backup manual do seu dispositivo.
> 
> 

### <a name="dual-controller-replacement-steps"></a>Etapas de substituição de controlador duplo
Este fluxo de trabalho é necessário quando ambos os controladores de saudação em seu dispositivo do Microsoft Azure StorSimple falharam. Isso pode acontecer em um data center em que o sistema de resfriamento Olá parou de funcionar e como resultado, ambos os controladores Olá falharem em um curto período de tempo. Dependendo se o dispositivo StorSimple Olá é desativado ou ativado e se você estiver usando um 8600 ou um modelo 8100, um conjunto diferente de etapas é necessário.

> [!IMPORTANT]
> Ele pode levar até 45 minutos too1 horas para Olá controlador toorestart e recuperar completamente de um procedimento de substituição de controlador duplo. tempo total de saudação para todo o procedimento hello, incluindo a conexão Olá cabos, é de aproximadamente 2,5 horas.
> 
> 

#### <a name="tooreplace-both-controller-modules"></a>tooreplace os módulos do controlador
1. Olá dispositivo estiver desativado, ignore esta etapa e passe toohello próxima etapa. Se Olá dispositivo for ativado, desative o dispositivo de saudação.
   
   1. Se você estiver usando um modelo 8600, desativar primeiro compartimento principal Olá e, em seguida, desligue Olá compartimento EBOD.
   2. Aguarde até que o dispositivo Olá desligue completamente. Olá todos os LEDs no hello parte posterior do dispositivo Olá será desligado.
2. Remova todos os cabos de rede de saudação que são conectados toohello portas de dados. Se você estiver usando um modelo 8600, também remova Olá que cabos de SAS que se conectam compartimento do hello compartimento principal toohello EBOD.
3. Remova os dois controladores de dispositivo do StorSimple hello. Para obter mais informações, consulte [Remover um controlador](#remove-a-controller).
4. Insira a substituição de fábrica Olá para o controlador 0 primeiro e, em seguida, insira o controlador 1. Para saber mais, consulte [insert a controller](#insert-a-controller). Isso dispara a lógica de substituição de controlador duplo hello. Para saber mais, consulte [dual controller replacement logic](#dual-controller-replacement-logic).
5. Enquanto a lógica de substituição de controlador Olá progride no plano de fundo hello, reconecte os cabos de saudação. Tomar cuidado tooconnect que todos os cabos de Olá Olá exatamente mesma maneira que estavam conectados antes da substituição de saudação. Consulte Olá instruções detalhadas para o modelo no hello cabo sua seção de dispositivo de [instalar seu dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md) ou [instalar seu dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md).
6. Ative o dispositivo StorSimple hello. Se estiver usando um modelo 8600:
   
   1. Certifique-se de que Olá compartimento EBOD é ativado primeiro.
   2. Aguarde até que a saudação compartimento EBOD está em execução.
   3. Ative o compartimento principal hello.
   4. Após o primeiro controlador de saudação reinicia e está em um estado íntegro, sistema hello serão executados.
      
      > [!NOTE]
      > Se você estiver monitorando dispositivo Olá por meio do console serial hello, você poderá ver várias reinicializações enquanto o controlador hello está se recuperando do procedimento de substituição de saudação. Quando o menu do console serial Olá aparece, você sabe que Olá substituição foi concluída. Se Olá menu não apareça dentro de 2,5 horas do início da substituição do controlador hello, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md).
      > 
      > 

## <a name="remove-a-controller"></a>Remover um controlador
Use Olá seguindo o procedimento tooremove um módulo do controlador com defeito do dispositivo StorSimple.

> [!NOTE]
> Olá ilustrações a seguir é para o controlador 0. No controlador 1, as ilustrações seriam invertidas.
> 
> 

#### <a name="tooremove-a-controller-module"></a>tooremove um módulo do controlador
1. Segure a trava do módulo Olá entre o polegar e o dedo indicador.
2. Aperte gentilmente seu polegar e o indicador toorelease juntos Olá travamento do controlador.
   
    ![Liberando a trava do controlador](./media/storsimple-controller-replacement/IC741047.png)
   
    **Figura 2** Liberando a trava do controlador
3. Use Olá trava como um controlador de saudação do identificador tooslide fora do chassi de saudação.
   
    ![Deslizando o controlador para fora do chassi](./media/storsimple-controller-replacement/IC741048.png)
   
    **Figura 3** controlador de saudação deslizante fora do chassi Olá

## <a name="insert-a-controller"></a>Inserir um controlador
Use Olá seguindo o procedimento tooinstall um módulo do controlador fornecido pela fábrica depois de remover um módulo com falha do seu dispositivo StorSimple.

#### <a name="tooinstall-a-controller-module"></a>tooinstall um módulo do controlador
1. Verifique toosee se não houver nenhum dano toohello conectores de interface. Não instale o módulo de saudação se algum dos pinos do conector Olá está danificado ou torto.
2. Deslize o módulo do controlador Olá para chassi Olá enquanto Olá chassi estiver completamente liberado. 
   
    ![Deslizando o controlador para dentro do chassi](./media/storsimple-controller-replacement/IC741053.png)
   
    **Figura 4** deslizante controlador no chassi Olá
3. Com o módulo do controlador Olá inserido, começar fechando travamento do hello ao módulo do controlador continuando toopush Olá no chassi hello. Olá trava controlador de saudação tooguide no lugar.
   
    ![Fechando a trava do controlador](./media/storsimple-controller-replacement/IC741054.png)
   
    **Figura 5** fechando travamento do controlador Olá
4. Terminar quando a trava Olá se encaixa no lugar. Olá **Okey** LED agora deverá estar ligado.  
   
   > [!NOTE]
   > Pode demorar até too5 minutos para o controlador de saudação e Olá tooactivate de LED.
   > 
   > 
5. tooverify substituição Olá for bem-sucedida, no hello Azure clássico, acesse muito**dispositivos** > **manutenção** > **Status do Hardware**e certifique-se de que o controlador 0 e o controlador 1 estão íntegros (o status é verde).

## <a name="identify-hello-active-controller-on-your-device"></a>Identificar controlador ativo de saudação do dispositivo
Há muitas situações, como substituição de controlador ou registro de dispositivo pela primeira vez, que exigem que você toolocate controlador ativo do hello em um dispositivo StorSimple. controlador ativo Olá processa todas as Olá disco rede e firmware operações. Você pode usar qualquer Olá controlador ativo do métodos tooidentify Olá a seguir:

* [Usar o controlador ativo do Olá Olá tooidentify de portal clássico do Azure](#use-the-azure-classic-portal-to-identify-the-active-controller)
* [Usar o Windows PowerShell para o controlador ativo do StorSimple tooidentify Olá](#use-windows-powershell-for-storsimple-to-identify-the-active-controller)
* [Verifique o controlador do dispositivo físico tooidentify Olá ativo Olá](#check-the-physical-device-to-identify-the-active-controller)

Cada um desses procedimentos é descrito abaixo.

### <a name="use-hello-azure-classic-portal-tooidentify-hello-active-controller"></a>Usar o controlador ativo do Olá Olá tooidentify de portal clássico do Azure
Olá portal clássico do Azure no, navegue muito**dispositivos** > **manutenção**e role toohello **controladores** seção. Aqui você pode verificar qual controlador está ativo.

![Identificar o controlador ativo no portal clássico do Azure](./media/storsimple-controller-replacement/IC752072.png)

**Figura 6** controlador ativo do hello mostrando de portal clássico do Azure

### <a name="use-windows-powershell-for-storsimple-tooidentify-hello-active-controller"></a>Usar o Windows PowerShell para o controlador ativo do StorSimple tooidentify Olá
Quando você acessar seu dispositivo por meio do console serial hello, uma mensagem de faixa é apresentada. mensagem faixa contém informações básicas do dispositivo como modelo Olá, nome, versão do software instalado e status do controlador de saudação que você está acessando. Olá a imagem a seguir mostra um exemplo de uma mensagem de faixa:

![Mensagem da faixa serial](./media/storsimple-controller-replacement/IC741098.png)

**Figura 7** Mensagem de cabeçalho mostrando o controlador 0 como ativo

Você pode usar o hello toodetermine de mensagem de faixa se Olá controlador que você está conectado toois ativo ou passivo.

### <a name="check-hello-physical-device-tooidentify-hello-active-controller"></a>Verifique o controlador do dispositivo físico tooidentify Olá ativo Olá
controlador ativo do hello tooidentify no seu dispositivo, localize o LED de saudação azul acima porta Olá parte traseira do compartimento principal Olá Olá DATA 5.

Se o LED estiver piscando, hello controlador está ativo e hello outro controlador está no modo de espera. Use Olá diagrama a seguir e como um auxílio de tabela.

![Backplane do compartimento primário do dispositivo com portas de dados](./media/storsimple-controller-replacement/IC741055.png)

**Figura 8** Parte traseira do compartimento primário com portas de dados e LEDs de monitoramento

| Rótulo | Descrição |
|:--- |:--- |
| 1-6 |Portas de rede DATA 0 – 5 |
| 7 |LED azul |

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).

