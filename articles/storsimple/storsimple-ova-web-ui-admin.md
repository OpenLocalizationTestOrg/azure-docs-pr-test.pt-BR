---
title: "web de matriz Virtual aaaStorSimple administração da interface do usuário | Microsoft Docs"
description: "Descreve como as tarefas de administração do tooperform básicas de dispositivos por meio da interface da web hello matriz Virtual StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a>Use Olá Web UI tooadminister sua matriz Virtual StorSimple
![fluxo do processo de instalação](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a>Visão geral
tutoriais de saudação neste artigo se aplicam a versão disponibilidade geral (GA) de março de 2016 em execução toohello Microsoft Azure StorSimple Virtual Array (também conhecido como Olá StorSimple no dispositivo virtual local). Este artigo descreve alguns dos fluxos de trabalho complexos hello e tarefas de gerenciamento que podem ser executadas em Olá matriz Virtual StorSimple. Você pode gerenciar Olá StorSimple matriz Virtual usando o serviço de Gerenciador de StorSimple Olá da interface do usuário (chamado tooas Olá IU do portal) e Olá interface da web local para o dispositivo de saudação. Este artigo enfoca tarefas Olá que você pode executar usando a interface da web hello.

Este artigo inclui Olá tutoriais a seguir:

* Obter chave de criptografia de dados de serviço Olá
* Solucionar problemas de erros de instalação de interface do usuário da Web
* Gerar um pacote de log
* Desligar ou reiniciar seu dispositivo

## <a name="get-hello-service-data-encryption-key"></a>Obter chave de criptografia de dados de serviço Olá
Uma chave de criptografia de dados de serviço é gerada quando você registra o dispositivo primeiro Olá serviço StorSimple Manager. Essa chave é necessária com hello serviço Registro tooregister chave dispositivos adicionais com hello serviço StorSimple Manager.

Se você esquecer sua chave de criptografia de dados de serviço e precisa tooretrieve, executar Olá seguintes etapas na interface de dispositivo de saudação da web local Olá registrado com o serviço.

#### <a name="tooget-hello-service-data-encryption-key"></a>chave de criptografia de dados de serviço do tooget Olá
1. Conecte-se a interface da web local toohello. Vá muito**configuração** > **as configurações de nuvem**.
2. Final Olá Olá página, clique em **chave de criptografia de dados de serviço Get**. Uma chave será exibida. Copie e salve essa chave.
   
    ![obter chave de criptografia de dados do serviço 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a>Solucionar problemas de erros de instalação de interface do usuário da Web
Em alguns casos quando você configura o dispositivo Olá Web local de saudação da interface do usuário, você pode executar em erros. toodiagnose e solucionar esses erros, você pode executar testes de diagnóstico de saudação.

#### <a name="toorun-hello-diagnostic-tests"></a>testes de diagnóstico toorun Olá
1. Olá interface da web local, vá muito**solução de problemas** > **testes de diagnóstico**.
   
    ![executar dignóstico 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. Final Olá Olá página, clique em **executar testes de diagnóstico**. Isso irá iniciar testes toodiagnose possíveis problemas com sua rede, dispositivo, proxy da web, hora ou as configurações de nuvem. Você será notificado de que o dispositivo hello está executando testes.
3. Após a conclusão dos testes de hello, Olá resultados serão exibidos. Olá, exemplo a seguir mostra os resultados de saudação de testes de diagnóstico. Observe que configurações de proxy da web hello não foram configuradas neste dispositivo e, portanto, o teste de proxy da web hello não foi executado. Olá a todos os outros testes para configurações de rede, servidor DNS, e as configurações de tempo foram bem-sucedidas.
   
    ![executar dignóstico 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a>Gerar um pacote de log
Um pacote de log é composto de todos os logs de saudação relevantes que podem ajudar a Microsoft Support na solução de problemas no dispositivo. Nesta versão, um pacote de log pode ser gerado por meio da interface do usuário da web local hello.

#### <a name="toogenerate-hello-log-package"></a>pacote de log toogenerate Olá
1. Olá interface da web local, vá muito**solução de problemas** > **logs do sistema**.
   
    ![gerar pacote de log 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. Final Olá Olá página, clique em **criar pacote de log**. Um pacote de saudação logs de sistema será criado. Isso levará alguns minutos.
   
    ![gerar pacote de log 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    Você será notificado depois de pacote de saudação é criado com êxito e Olá página será atualizada quando o pacote de saudação foi criado de data e hora de saudação do tooindicate.
   
    ![gerar pacote de log 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. Clique em **Baixar pacote de log**. Um pacote compactado será baixado em seu sistema.
   
    ![gerar pacote de log 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. Você pode descompactar pacote de log baixados Olá e exibir arquivos de log do sistema de saudação.

## <a name="shut-down-and-restart-your-device"></a>Desligue e reinicie seu dispositivo
Você pode desligar ou reiniciar seu dispositivo virtual usando a interface da web local hello. É recomendável que, antes de reiniciar, levar volumes hello ou compartilhamentos offline no host Olá Olá, em seguida, o dispositivo. Isso minimizará a possibilidade de dados corrompidos. 

#### <a name="tooshut-down-your-virtual-device"></a>tooshut seu dispositivo virtual
1. Olá interface da web local, vá muito**manutenção** > **as configurações de energia**.
2. Final Olá Olá página, clique em **desligamento**.
   
    ![desligamento de dispositivo 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. Um aviso será exibido informando que um desligamento do dispositivo Olá interromperá qualquer e/s que estava em andamento, resultando em um tempo de inatividade. Clique o ícone de verificação Olá ![ícone de verificação](./media/storsimple-ova-web-ui-admin/image3.png).
   
    ![aviso de desligamento de dispositivo](./media/storsimple-ova-web-ui-admin/image37.png)
   
    Você será notificado que desligamento Olá foi iniciado.
   
    ![o desligamento de dispositivo foi iniciado](./media/storsimple-ova-web-ui-admin/image38.png)
   
    dispositivo Olá será encerrado agora. Se você quiser toostart seu dispositivo, você precisará toodo que, por meio de Olá Gerenciador Hyper-V.

#### <a name="toorestart-your-virtual-device"></a>toorestart seu dispositivo virtual
1. Olá interface da web local, vá muito**manutenção** > **as configurações de energia**.
2. Final Olá Olá página, clique em **reiniciar**.
   
    ![reinicialização do dispositivo](./media/storsimple-ova-web-ui-admin/image36.png)
3. Um aviso será exibido informando que reiniciar o dispositivo Olá interromperá qualquer IOs que estavam em andamento, resultando em um tempo de inatividade. Clique o ícone de verificação Olá ![ícone de verificação](./media/storsimple-ova-web-ui-admin/image3.png).
   
    ![aviso de reinicialização](./media/storsimple-ova-web-ui-admin/image37.png)
   
    Você será notificado de que a reinicialização Olá foi iniciada.
   
    ![reinicialização iniciada](./media/storsimple-ova-web-ui-admin/image39.png)
   
    Enquanto Olá reinicialização está em andamento, você perderá Olá conexão toohello da interface do usuário. Você pode monitorar Olá reinicialização atualizando Olá UI periodicamente. Como alternativa, você pode monitorar o status de reinicialização do dispositivo Olá por meio de saudação Gerenciador Hyper-V.

## <a name="next-steps"></a>Próximas etapas
Saiba como muito[use Olá toomanage do serviço StorSimple Manager seu dispositivo](storsimple-virtual-array-manager-service-administration.md).

