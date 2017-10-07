---
title: controladores de dispositivo aaaManage StorSimple 8000 series | Microsoft Docs
description: Saiba como toostop, reiniciar, desligar ou redefinir os controladores de dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/19/2017
ms.author: alkohli
ms.openlocfilehash: 5c59582b7ccf7cfeae9e7efbd0e4df9dc1d3871c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>Gerenciar controladores de dispositivo StorSimple

## <a name="overview"></a>Visão geral

Este tutorial descreve as operações diferentes de saudação que podem ser executadas em seus controladores de dispositivo StorSimple. os controladores de saudação em seu dispositivo StorSimple são controladores redundantes (par) em uma configuração ativa-passiva. Em um determinado momento, somente um controlador está ativo e está processando todas as operações de disco e rede hello. Olá outro controlador está em um modo passivo. Se o controlador ativo Olá falhar, controlador passivo Olá automaticamente se torna ativo.

Este tutorial inclui os controladores de dispositivo de saudação do toomanage instruções passo a passo usando o:

* **Controladores** folha para seu dispositivo no hello serviço do Gerenciador de dispositivos do StorSimple.
* Windows PowerShell para StorSimple.

É recomendável que você gerencie os controladores de dispositivo Olá por meio do serviço do Gerenciador de dispositivos de StorSimple hello. Se uma ação só pode ser executada usando o Windows PowerShell para StorSimple, tutorial Olá faz uma observação sobre ela.

Depois de ler este tutorial, você poderá:

* Reiniciar ou desligar um controlador de dispositivo StorSimple
* Desligar um dispositivo StorSimple
* Redefinir os padrões de toofactory do dispositivo StorSimple

## <a name="restart-or-shut-down-a-single-controller"></a>Reiniciar ou desligar um único controlador
Uma reinicialização ou um desligamento de controlador não é necessário como parte da operação normal do sistema. As operações de desligamento para um controlador de dispositivo único são comuns apenas em casos em que um componente de hardware de dispositivo com falha requer substituição. Uma reinicialização de controlador também pode ser necessária em uma situação em que o desempenho é afetado pelo uso excessivo de memória ou controlador com defeito. Toorestart um controlador também pode ser necessário após a substituição de um controlador com êxito, se você deseja tooenable e Olá substituído controlador de teste.

Reiniciar um dispositivo não é tooconnected interrupções iniciadores, supondo que o controlador passivo hello está disponível. Se o controlador passivo não está disponível ou desativado, reiniciando Olá active controlador pode resultar na interrupção de saudação do serviço e o tempo de inatividade.

> [!IMPORTANT]
> * **Um controlador em execução nunca deve ser fisicamente removido, pois isso resultaria em uma perda de redundância e maior risco de tempo de inatividade.**
> * Olá procedimento a seguir aplica-se apenas toohello dispositivo físico StorSimple. Para obter informações sobre como toostart, pare e reinicie Olá StorSimple Appliance de nuvem, consulte [trabalhar com o dispositivo de nuvem Olá](storsimple-8000-cloud-appliance-u2.md##work-with-the-storsimple-cloud-appliance).

Você pode reiniciar ou desligar um controlador de dispositivo único por meio de saudação do Azure portal de serviço do Gerenciador de dispositivos de StorSimple hello ou o Windows PowerShell para StorSimple.

toomanage os controladores de dispositivo de saudação portal do Azure, executar Olá seguintes etapas.

#### <a name="toorestart-or-shut-down-a-controller-in-azure-portal"></a>toorestart ou desligar um controlador no portal do Azure
1. O serviço do Gerenciador de dispositivos de StorSimple, ir muito**dispositivos**. Selecione o dispositivo na lista de saudação de dispositivos. 

    ![Escolha um dispositivo](./media/storsimple-8000-manage-device-controller/manage-controller1.png)

2. Vá muito**Configurações > controladores**.
   
    ![Verificar a integridade dos controladores do dispositivo StorSimple](./media/storsimple-8000-manage-device-controller/manage-controller2.png)
3. Em Olá **controladores** folha, verifique se que o status de saudação de ambos os controladores de saudação do dispositivo é **Íntegro**. Selecione um controlador, clique com botão direito do mouse e escolha **Reiniciar** ou **Desligar**.

    ![Selecione reiniciar ou desligar controladores do dispositivo StorSimple](./media/storsimple-8000-manage-device-controller/manage-controller3.png)

4. Um trabalho é criado toorestart ou desligar controlador hello e você verá avisos aplicáveis, se houver. toomonitor Olá reinicialização ou desligamento, vá muito**Service > logs de atividade** e, em seguida, filtrar pelo serviço de tooyour específicas de parâmetros. Se um controlador estava desligado, você precisará toopush Olá power botão tooturn em Olá controlador tooturn-la no.

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart ou desligar um controlador no Windows PowerShell para StorSimple
Execute Olá tooshut as etapas a seguir para baixo ou reiniciar um único controlador em seu dispositivo StorSimple de saudação do Windows PowerShell para StorSimple.

1. Acessar o dispositivo Olá através do console serial hello ou uma sessão telnet de um computador remoto. tooconnect tooController 0 ou controlador 1, execute as etapas de saudação em [console serial do dispositivo Use PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. No menu do console serial hello, escolha a opção 1, **entrar com acesso completo**.
3. Na mensagem de faixa Olá, tome nota do controlador Olá muito estiver conectado (controlador 0 ou controlador 1) e se Olá active controlador está ou Olá passivo (em espera).
   
   * tooshut para baixo de um único controlador, no prompt de hello, digite:
     
       `Stop-HcsController`
     
       Isso fecha controlador Olá que você está conectado. Se você parar o controlador ativo hello, dispositivo Olá falha em controlador passivo toohello.

   * toorestart um controlador, no prompt de hello, digite:
     
       `Restart-HcsController`
     
       Isso reinicia o controlador de saudação que você está conectado. Se você reiniciar o controlador ativo hello, ocorre o failover controlador passivo toohello antes de reiniciar hello.

## <a name="shut-down-a-storsimple-device"></a>Desligar um dispositivo StorSimple

Esta seção explica como tooshut para baixo de um dispositivo StorSimple com falha de um computador remoto ou um execução. Um dispositivo é desativado depois que ambos os controladores de dispositivo Olá estão desligados. Desligar um dispositivo é feita ao dispositivo Olá for movido fisicamente ou retirado de serviço.

> [!IMPORTANT]
> Antes de desligar o dispositivo Olá, verificar a integridade de saudação de componentes do dispositivo hello. Navegue tooyour dispositivo e, em seguida, clique em **Configurações > integridade do Hardware**. Em Olá **hardware e Status de integridade** folha, verifique se que o status de saudação LED de todos os componentes de saudação é verde. Apenas dispositivos íntegros mostram status verde. Se seu dispositivo está sendo desligado tooreplace um componente de mau funcionamento, você verá um falha (vermelho) ou um estado degradado (amarelo) para Olá respectivos componente (s).


#### <a name="tooshut-down-a-storsimple-device"></a>tooshut um dispositivo StorSimple

1. Saudação de uso [reiniciar ou desligar um controlador](#restart-or-shut-down-a-single-controller) tooidentify procedimento e desligar o controlador passivo de saudação em seu dispositivo. Você pode executar esta operação no hello portal do Azure ou no Windows PowerShell para StorSimple.
2. Repita Olá acima tooshut etapa para baixo o controlador ativo hello.
3. Você deve agora examine Olá volta plano do dispositivo hello. Depois de dois controladores de saudação estiverem completamente desligados, hello LEDs de ambos os controladores Olá piscarão na cor vermelha. Se você precisar tooturn dispositivo Olá completamente nesse momento, Olá invertido interruptores nos módulos energia e resfriamento (PCMs) toohello OFF posição. Isso deve desativar dispositivo hello.

## <a name="reset-hello-device-toofactory-default-settings"></a>Redefinir as configurações padrão do hello dispositivo toofactory

> [!IMPORTANT]
> Se você precisar tooreset as configurações padrão do dispositivo toofactory, entre em contato com o Microsoft Support. procedimento Olá descrito a seguir deve ser usado somente em conjunto com o Microsoft Support.

Este procedimento descreve como tooreset as configurações padrão do Microsoft Azure StorSimple dispositivo toofactory usando o Windows PowerShell para StorSimple.
Redefinir um dispositivo remove todos os dados e configurações de cluster inteiro de saudação por padrão.

Execute as configurações padrão do Microsoft Azure StorSimple dispositivo toofactory de Olá tooreset as etapas a seguir:

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset Olá toodefault configurações de dispositivo no Windows PowerShell para StorSimple
1. Acessar o dispositivo Olá através do seu console serial. Verificar Olá tooensure de mensagem de faixa que você está conectado toohello **Active** controlador.
2. No menu do console serial hello, escolha a opção 1, **entrar com acesso completo**.
3. No prompt de hello, digite Olá após o comando tooreset Olá todo o cluster, removendo todas as configurações de controlador, metadados e dados:
   
    `Reset-HcsFactoryDefault`
   
    tooinstead redefinir um único controlador, use Olá [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet com hello `-scope` parâmetro.)
   
    sistema de saudação será reiniciado várias vezes. Você será notificado quando Olá redefinição foi concluída com êxito. Dependendo do modelo do sistema hello, pode levar 45 a 60 minutos para um dispositivo 8100 e 60 a 90 minutos para um toofinish 8600 esse processo.
   
## <a name="questions-and-answers-about-managing-device-controllers"></a>Perguntas e respostas sobre como gerenciar controladores de dispositivo
Nesta seção, podemos resumiu alguns Olá perguntas frequentes sobre como gerenciar controladores do dispositivo StorSimple.

**P.** O que acontece se ambos Olá controladores em meu dispositivo estão íntegro e ativado e eu reiniciar ou desligar o controlador ativo Olá?

**A.** Se ambos os controladores de saudação em seu dispositivo estiverem íntegros e ativados, você será solicitado para confirmação. Você pode optar por:

* **Reinicie o controlador ativo Olá** – você será notificado que reiniciar um controlador ativo causados Olá dispositivo toofail em controlador passivo toohello. Olá reinicializações do controlador.
* **Desligar um controlador ativo** – Você será notificado de que desligar um controlador ativo resultará em tempo de inatividade. Você também precisa toopush Olá botão liga / desliga Olá dispositivo tooturn no controlador de saudação.

**P.** O que acontece se o controlador passivo de saudação em meu dispositivo está indisponível ou desativado desativado e eu reiniciar ou desligar o controlador ativo Olá?

**A.** Se o controlador passivo de saudação em seu dispositivo está indisponível ou desativado e você optar por:

* **Reinicie o controlador ativo Olá** – você será notificado que continuar a operação de saudação resultará em uma interrupção temporária do serviço Olá, e você for solicitada uma confirmação.
* **Desligar um controlador ativo** – você será notificado que operação contínua de saudação resulta em tempo de inatividade. Você também precisa toopush Olá botão liga / desliga uma ou ambas as tooturn controladores no dispositivo de saudação. Você recebe uma solicitação para fornecer sua confirmação.

**P.** Quando a saudação controlador reinicialização ou desligamento falha tooprogress?

**A.** Reiniciar ou desligar um controlador pode falhar se:

* Uma atualização do dispositivo está em andamento.
* Uma reinicialização de controlador já está em andamento.
* Um desligamento do controlador já está em andamento.

**P.** Como saber se um controlador foi reiniciado ou desligado?

**A.** Você pode verificar o status do controlador Olá na folha de controlador. status do controlador Olá indicará se um controlador está no processo de saudação de reiniciar ou desligar. Além disso, Olá **alertas** folha contêm um alerta informativo se o controlador de saudação é reiniciado ou desligado. operações de reinicialização e desligamento do controlador Olá também são registradas nos logs de atividades de saudação. Para obter mais informações sobre logs de atividades, ir muito[exibir logs de atividade Olá](storsimple-8000-service-dashboard.md#view-the-activity-logs).

**P.** Há qualquer toohello impacto e/s como resultado de failover do controlador?

**A.** conexões de TCP Olá entre os iniciadores e o controlador ativo serão redefinidas como resultado de failover do controlador, mas serão restabelecidas quando o controlador passivo Olá assume a operação. Pode haver uma pausa temporária (menos de 30 segundos) na atividade de e/s entre os iniciadores e o dispositivo Olá durante saudação dessa operação.

**P.** Como devolver meu controlador tooservice depois que ele foi desligado e removido?

**A.** tooreturn tooservice um controlador, você deve inseri-lo no chassi Olá conforme descrito em [substituir um módulo do controlador em seu dispositivo StorSimple](storsimple-8000-controller-replacement.md).

## <a name="next-steps"></a>Próximas etapas
* Se você encontrar algum problema com os controladores de dispositivo StorSimple que você não conseguir resolver usando procedimentos de saudação listados neste tutorial, [entre em contato com o Microsoft Support](storsimple-8000-contact-microsoft-support.md).
* toolearn mais sobre como usar o serviço do Gerenciador de dispositivos de StorSimple hello, ir muito[Use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

