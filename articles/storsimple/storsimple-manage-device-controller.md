---
title: controladores de dispositivo do StorSimple aaaManage | Microsoft Docs
description: Saiba como toostop, reiniciar, desligar ou redefinir os controladores de dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4ee989d0-956f-4c14-951e-fd4e490ea09d
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/11/2016
ms.author: alkohli
ms.openlocfilehash: 9a86aa0f4a8fd96c36df206774972602c47a49a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>Gerenciar controladores de dispositivo StorSimple
## <a name="overview"></a>Visão geral
Este tutorial descreve as operações diferentes de saudação que podem ser executadas em seus controladores de dispositivo StorSimple. os controladores de saudação em seu dispositivo StorSimple são controladores redundantes (par) em uma configuração ativa-passiva. Em um determinado momento, somente um controlador está ativo e está processando todas as operações de disco e rede hello. Olá outro controlador está em um modo passivo. Se o controlador ativo Olá falhar, controlador passivo Olá torna-se ativo automaticamente.

Este tutorial inclui os controladores de dispositivo de saudação do toomanage instruções passo a passo usando o:

* **Controladores** seção Olá **manutenção** página Olá serviço StorSimple Manager
* Windows PowerShell para StorSimple.

É recomendável que você gerencie os controladores de dispositivo Olá por meio do serviço do StorSimple Manager hello. Se uma ação só pode ser executada usando o Windows PowerShell para StorSimple, tutorial Olá faz uma observação sobre ela.

Depois de ler este tutorial, você poderá:

* Reiniciar ou desligar um controlador de dispositivo StorSimple
* Desligar um dispositivo StorSimple
* Redefinir os padrões de toofactory do dispositivo StorSimple

## <a name="restart-or-shut-down-a-single-controller"></a>Reiniciar ou desligar um único controlador
Uma reinicialização ou um desligamento de controlador não é necessário como parte da operação normal do sistema. As operações de desligamento para um controlador de dispositivo único são comuns apenas em casos em que um componente de hardware de dispositivo com falha requer substituição. Uma reinicialização de controlador também pode ser necessária em uma situação em que o desempenho é afetado pelo uso excessivo de memória ou controlador com defeito. Toorestart um controlador também pode ser necessário após a substituição de um controlador com êxito, se você deseja tooenable e Olá substituído controlador de teste.

Reiniciar um dispositivo não é tooconnected interrupções iniciadores, supondo que o controlador passivo hello está disponível. Se o controlador passivo não está disponível ou desativado, reiniciando Olá active controlador pode resultar na interrupção de saudação do serviço e o tempo de inatividade.

> [!IMPORTANT]
> * **Um controlador em execução nunca deve ser fisicamente removido, pois isso resultaria em uma perda de redundância e maior risco de tempo de inatividade.**
> * Olá procedimento a seguir aplica-se apenas toohello dispositivo físico StorSimple. Para obter informações sobre como toostart, pare e reinicie Olá o dispositivo virtual, consulte [trabalhar com o dispositivo virtual Olá](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device).
> 
> 

Você pode reiniciar ou desligar um controlador de dispositivo único usando Olá portal clássico do Azure do serviço do StorSimple Manager hello ou o Windows PowerShell para StorSimple

toomanage os controladores de dispositivo de saudação portal clássico do Azure, executar Olá seguintes etapas.

#### <a name="toorestart-or-shut-down-a-controller-in-classic-portal"></a>toorestart ou desligar um controlador no portal clássico
1. Navegue muito**dispositivos > manutenção**.
2. Vá muito**Status do Hardware** e verificar se o status de saudação de ambos os controladores de saudação em seu dispositivo está **Íntegro**.
   
    ![Verificar a integridade dos controladores do dispositivo StorSimple](./media/storsimple-manage-device-controller/IC766017.png)
3. De baixo Olá Olá **manutenção** , clique em **gerenciar controladores**.
   
    ![Gerenciar controladores de dispositivo StorSimple](./media/storsimple-manage-device-controller/IC766018.png)</br>
   
   > [!NOTE]
   > Se você não conseguir ver **gerenciar controladores**, em seguida, você precisa tooinstall atualizações. Para obter mais informações, consulte [Atualizar seu dispositivo StorSimple](storsimple-update-device.md).
   > 
   > 
4. Em Olá **alterar configurações do controlador** caixa de diálogo caixa, Olá a seguir:
   
   1. De saudação **selecionar controlador** lista suspensa, o controlador de saudação selecione que você deseja toomanage. Opções de saudação são controlador 0 e 1. Esses controladores também são identificados como ativo ou passivo.
      
      > [!NOTE]
      > Um controlador não pode ser gerenciado se ele estiver indisponível ou desativado, e ele não aparecerá na lista suspensa de saudação.
      > 
      > 
   2. De saudação **Selecionar ação** lista suspensa, escolha **reinicialização controlador** ou **desligar controlador**.
      
       ![Reiniciar o controlador passivo do dispositivo StorSimple](./media/storsimple-manage-device-controller/IC766020.png)
   3. Clique o ícone de verificação Olá ![Ícone de verificação](./media/storsimple-manage-device-controller/IC740895.png).

Isso irá reiniciar ou desligar o controlador de saudação. Olá tabela a seguir resume os detalhes de saudação do que acontece dependendo das seleções Olá feitas no hello **alterar configurações do controlador** caixa de diálogo.  

| Seleção # | Se você optar por... | Acontecerá isso. |
| --- | --- | --- |
| 1. |Reinicie controlador passivo hello. |Um trabalho será criado controlador de saudação toorestart, e você será notificado quando o trabalho de saudação é criado com êxito. Isso iniciará a reinicialização de controlador hello. Você pode monitorar o processo de reinicialização Olá acessando **serviço > Painel de controle > Exibir logs de operação** e filtrando pelo serviço de tooyour específicas de parâmetros. |
| 2. |Reinicie o controlador ativo hello. |Você verá Olá aviso a seguir: "Se você reiniciar o controlador ativo hello, dispositivo Olá fará failover em controlador passivo toohello. Você deseja toocontinue?" </br>Se você escolher tooproceed com essa operação, o hello próximas etapas serão toorestart de toothose idênticos usado Olá controlador passivo (consulte a seleção 1). |
| 3. |Desligar o controlador passivo hello. |Você verá a seguinte mensagem de saudação: "depois do desligamento ser concluído, será preciso toopush Olá botão liga em seu controlador tooturn-lo. Tem certeza de que deseja tooshut para este controlador?" </br>Se você escolher tooproceed com essa operação, o hello próximas etapas serão toorestart de toothose idênticos usado Olá controlador passivo (consulte a seleção 1). |
| 4. |Desligar o controlador ativo hello. |Você verá a seguinte mensagem de saudação: "depois do desligamento ser concluído, será preciso toopush Olá botão liga em seu controlador tooturn-lo. Tem certeza de que deseja tooshut para este controlador?" </br>Se você escolher tooproceed com essa operação, o hello próximas etapas serão toorestart de toothose idênticos usado Olá controlador passivo (consulte a seleção 1). |

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart ou desligar um controlador no Windows PowerShell para StorSimple
Execute Olá tooshut as etapas a seguir para baixo ou reiniciar um único controlador em seu dispositivo StorSimple do hello portal clássico do Azure.

1. Acessar o dispositivo hello usando o console serial hello ou uma sessão telnet de um computador remoto. Conecte-se tooController 0 ou controlador 1 por Olá seguir as etapas em [console serial do dispositivo Use PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. No menu do console serial hello, escolha a opção 1, **entrar com acesso completo**.
3. Na mensagem de faixa Olá, tome nota do controlador Olá muito estiver conectado (controlador 0 ou controlador 1) e se Olá active controlador está ou Olá passivo (em espera).
   
   * tooshut para baixo de um único controlador, no prompt de hello, digite:
     
       `Stop-HcsController`
     
       Isso desligará controlador Olá que você está conectado. Se você parar o controlador ativo hello, em seguida, ele faz failover controlador passivo toohello antes de desligar.
   * toorestart um controlador, no prompt de hello, digite:
     
       `Restart-HcsController`
     
       Isso reiniciará o controlador de saudação que você está conectado. Se você reiniciar o controlador ativo hello, ele falhará em controlador passivo toohello antes de reiniciar hello.

## <a name="shut-down-a-storsimple-device"></a>Desligar um dispositivo StorSimple
Esta seção explica como tooshut para baixo de um dispositivo StorSimple com falha de um computador remoto ou um execução. Um dispositivo é desativado após desligar de ambos os controladores de dispositivo de saudação. Desligar um dispositivo é feita ao dispositivo hello está sendo movido fisicamente ou retirado de serviço.

> [!IMPORTANT]
> Antes de desligar o dispositivo Olá, verificar a integridade de saudação de componentes do dispositivo hello. Navegue muito**dispositivos > manutenção > Status do Hardware** e verificar se o status de saudação LED de todos os componentes de saudação está verde. Somente um dispositivo íntegro terá um status em verde. Se seu dispositivo está sendo desligado tooreplace um componente de mau funcionamento, você verá um falha (vermelho) ou um estado degradado (amarelo) para Olá respectivos componente (s).
> 
> 

#### <a name="tooshut-down-a-storsimple-device"></a>tooshut um dispositivo StorSimple
1. Saudação de uso [reiniciar ou desligar um controlador](#restart-or-shut-down-a-single-controller) tooidentify procedimento e desligar o controlador passivo de saudação em seu dispositivo. Você pode executar esta operação no hello portal clássico do Azure ou no Windows PowerShell para StorSimple.
2. Repita Olá acima tooshut etapa para baixo o controlador ativo hello.
3. Agora será necessário toolook em Olá plano posterior do dispositivo hello. Depois de dois controladores de saudação estiverem completamente desligados, hello LEDs de ambos os controladores Olá piscarão na cor vermelha. Se você precisar tooturn dispositivo Olá completamente nesse momento, Olá invertido interruptores nos módulos energia e resfriamento (PCMs) toohello OFF posição. Isso deve desativar dispositivo hello.

<!--#### tooshut down a StorSimple device in Windows PowerShell for StorSimple

1. Connect toohello serial console of hello StorSimple device by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-serial-console).

1. In hello serial console menu, verify from hello banner message that hello controller you are connected toois hello passive controller. If you are connected toohello active controller, disconnect from this controller and connect toohello other controller.

1. In hello serial console menu, choose option 1, **log in with full access**.

1. At hello prompt, type:

    `Stop-HCSController`

    This should shut down hello current controller. tooverify whether hello shutdown has finished, check hello back of hello device. hello controller status LED should be solid red.

1. Repeat steps 1 through 4 tooconnect toohello active controller and then shut it down.

1. After both hello controllers are completely shut down, hello status LEDs on both should be blinking red. If you need tooturn off hello device completely at this time, flip hello power switches on both Power and Cooling Modules (PCMs) toohello OFF position.-->

## <a name="reset-hello-device-toofactory-default-settings"></a>Redefinir as configurações padrão do hello dispositivo toofactory
> [!IMPORTANT]
> Se você precisar tooreset as configurações padrão do dispositivo toofactory, entre em contato com o Microsoft Support. procedimento Olá descrito a seguir deve ser usado somente em conjunto com o Microsoft Support.
> 
> 

Este procedimento descreve como tooreset as configurações padrão do Microsoft Azure StorSimple dispositivo toofactory usando o Windows PowerShell para StorSimple.
Redefinir um dispositivo remove todos os dados e configurações de cluster inteiro de saudação por padrão.

Execute as configurações padrão do Microsoft Azure StorSimple dispositivo toofactory de Olá tooreset as etapas a seguir:

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset Olá toodefault configurações de dispositivo no Windows PowerShell para StorSimple
1. Acessar o dispositivo Olá através do seu console serial. Verifique tooensure de mensagem de faixa Olá que você é o controlador ativo toohello conectado.
2. No menu do console serial hello, escolha a opção 1, **entrar com acesso completo**.
3. No prompt de hello, digite Olá após o comando tooreset Olá todo o cluster, removendo todas as configurações de controlador, metadados e dados:
   
    `Reset-HcsFactoryDefault`
   
    tooinstead redefinir um único controlador, use Olá [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet com hello `-scope` parâmetro.)
   
    sistema de saudação será reiniciado várias vezes. Você será notificado quando Olá redefinição foi concluída com êxito. Dependendo do modelo do sistema hello, pode levar 45 a 60 minutos para um dispositivo 8100 e 60 a 90 minutos para um toofinish 8600 esse processo.
   
   > [!TIP]
   > * Se você estiver usando Update 1.2 ou anterior, use Olá `–SkipFirmwareVersionCheck` verificação de versão de firmware do parâmetro tooskip hello (caso contrário, você verá um erro de incompatibilidade de firmware: redefinição de fábrica não pode continuar devido a incompatibilidade de tooa em versões de firmware de saudação. ).
   > * o procedimento de redefinição de fábrica Olá pode falhar para dispositivos de StorSimple que estão executando a atualização 1 ou 1.1 no portal do governo hello e executaram uma substituição de controlador único ou duplo com êxito (com controladores de substituição que foram enviados com pré-atualização 1 software). Isso ocorre quando a redefinição de fábrica Olá imagem é validada para a presença de saudação de um arquivo de SHA1 no controlador de saudação que não existe para o software de pré-atualização 1. Se você vir esta fábrica redefinição falha, entre em contato com o Microsoft Support tooassist com hello próximas etapas. Esse problema não seja visto com os controladores de substituição que foram enviados da fábrica Olá com atualização 1 ou posterior software.
   > 
   > 

## <a name="questions-and-answers-about-managing-device-controllers"></a>Perguntas e respostas sobre como gerenciar controladores de dispositivo
Nesta seção, podemos resumiu alguns Olá perguntas frequentes sobre como gerenciar controladores do dispositivo StorSimple.

**P.** O que acontece se ambos Olá controladores em meu dispositivo estão íntegro e ativado e eu reiniciar ou desligar o controlador ativo Olá?

**A.** Se ambos os controladores de saudação em seu dispositivo estiverem íntegros e ativados, você será solicitado para confirmação. Você pode optar por:

* **Reinicie o controlador ativo Olá** – você será notificado que reiniciar um controlador ativo fará com que Olá dispositivo toofail sobre o controlador passivo toohello. Olá controlador será reiniciado.
* **Desligar um controlador ativo** – você será notificado de que desligar um controlador ativo resultará em tempo de inatividade. Você também precisará toopush Olá botão liga / desliga Olá dispositivo tooturn no controlador de saudação.

**P.** O que acontece se o controlador passivo de saudação em meu dispositivo está indisponível ou desativado desativado e eu reiniciar ou desligar o controlador ativo Olá?

**A.** Se o controlador passivo de saudação em seu dispositivo está indisponível ou desativado e você optar por:

* **Reinicie o controlador ativo Olá** – você será notificado que continuar a operação de saudação resultará em uma interrupção temporária do serviço Olá, e você será solicitado a confirmar.
* **Desligar um controlador ativo** – você será notificado que continuar a operação de saudação resulta em tempo de inatividade e que você precisará toopush Olá botão liga / desliga uma ou ambas as tooturn controladores no dispositivo de saudação. Será solicitada a sua confirmação.

**P.** Quando a saudação controlador reinicialização ou desligamento falha tooprogress?

**A.** Reiniciar ou desligar um controlador pode falhar se:

* Uma atualização do dispositivo está em andamento.
* Uma reinicialização de controlador já está em andamento.
* Um desligamento do controlador já está em andamento.

**P.** Como saber se um controlador foi reiniciado ou desligado?

**A.** Você pode verificar o status do controlador Olá na página de manutenção de saudação. status do controlador Olá indicará se um controlador foi reiniciado ou desligado. Além disso, página de alertas de saudação conterá um alerta informativo se o controlador de saudação foi reiniciado ou desligado. operações de reinicialização e desligamento do controlador Olá também são registradas nos logs de operação de saudação. Para obter mais informações sobre logs de operação, vá muito[exibir logs de operação Olá](storsimple-service-dashboard.md#view-the-operations-logs).

**P.** Há qualquer toohello impacto e/SS como resultado de failover do controlador?

**A.** conexões de TCP Olá entre os iniciadores e o controlador ativo serão redefinidas como resultado de failover do controlador, mas serão restabelecidas quando o controlador passivo Olá assume a operação. Pode haver uma pausa temporária (menos de 30 segundos) na atividade de e/s entre os iniciadores e o dispositivo Olá durante saudação dessa operação.

**P.** Como devolver meu controlador tooservice depois que ele foi desligado e removido?

**A.** tooreturn tooservice um controlador, você deve inseri-lo no chassi Olá conforme descrito em [substituir um módulo do controlador em seu dispositivo StorSimple](storsimple-controller-replacement.md).

## <a name="next-steps"></a>Próximas etapas
* Se você encontrar algum problema com os controladores de dispositivo StorSimple que você não conseguir resolver usando procedimentos de saudação listados neste tutorial, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md).
* toolearn mais sobre como usar o serviço StorSimple Manager hello, ir muito[Use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).

