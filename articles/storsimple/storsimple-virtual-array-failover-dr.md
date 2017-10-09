---
title: "aaaStorSimple Array Virtual desastres recuperação e failover de dispositivo | Microsoft Docs"
description: Saiba mais sobre como toofailover sua matriz Virtual StorSimple.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 3c1f9c62-af57-4634-a0d8-435522d969aa
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f125efd1ffb94489cdfa7cfaafae7d57cc10131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-and-device-failover-for-your-storsimple-virtual-array-via-azure-portal"></a>Failover de dispositivo e recuperação de desastre para o StorSimple Virtual Array via portal do Azure

## <a name="overview"></a>Visão geral
Este artigo descreve a recuperação de desastres Olá para sua matriz de Virtual do Azure StorSimple incluindo Olá detalhada da Microsoft etapas toofail em matriz virtual tooanother. Um failover permite que você toomove seus dados de um *fonte* dispositivo no hello datacenter tooa *destino* dispositivo. Olá dispositivo de destino pode ser localizado no hello mesma ou em um local geográfico diferente. failover de dispositivo de saudação é para todo dispositivo de saudação. Durante o failover, dados na nuvem para dispositivo de origem Olá Olá alteram toothat de propriedade do dispositivo de destino hello.

Este artigo é aplicável tooStorSimple matrizes Virtual. toofail em um dispositivo da 8000 série, vá muito[dispositivo failover e recuperação de desastres do seu dispositivo StorSimple](storsimple-device-failover-disaster-recovery.md).

## <a name="what-is-disaster-recovery-and-device-failover"></a>O que é recuperação de desastre e failover de dispositivo?

Em um cenário de recuperação de desastre, dispositivo primário Olá parará de funcionar. Nesse cenário, você pode mover dados de nuvem de saudação associados Olá dispositivo com falha tooanother dispositivo. Você pode usar o dispositivo primário hello como Olá *fonte* e especifique outro dispositivo como Olá *destino*. Esse processo é chamado tooas Olá *failover*. Durante o failover, Olá a todos os volumes ou compartilhamentos de saudação do dispositivo de origem Olá alterar a propriedade e são transferidos toohello dispositivo de destino. Nenhuma filtragem de dados de saudação é permitido.

Recuperação de desastres é modelada como uma restauração completa do dispositivo usando calor Olá mapa com base em camadas e de controle. Um mapa de calor é definido, atribuindo um toohello de valor de calor com base em dados de leitura e gravação padrões. Esse calor mapear e camadas Olá menor calor dados partes toohello nuvem primeiro mantendo Olá partes de dados de calor alta (mais usado) na camada de saudação local. Durante uma recuperação de desastres, StorSimple usa toorestore de mapa de calor hello e realimentar dados saudação da nuvem de saudação. dispositivo Olá busca todos os volumes/compartilhamento Olá no último backup recente do hello (conforme determinado internamente) e executa uma restauração do backup. matriz virtual Olá orquestra todo o processo de recuperação de desastres hello.

> [!IMPORTANT]
> dispositivo de origem de saudação é excluído no final de saudação do failover de dispositivo e, portanto, não há suporte para um failback.
> 
> 

Recuperação de desastres é organizada por meio do recurso de failover de dispositivo hello e é iniciada do hello **dispositivos** folha. Esta folha tabula todos Olá StorSimple dispositivos conectados tooyour dispositivo o serviço StorSimple Manager. Para cada dispositivo, você pode ver o nome amigável do hello, status, capacidade provisionada e máximo, tipo e modelo.

## <a name="prerequisites-for-device-failover"></a>Pré-requisitos para failover de dispositivo

### <a name="prerequisites"></a>Pré-requisitos

Para um failover de dispositivo, certifique-se de que Olá pré-requisitos a seguir forem atendidas:

* dispositivo de origem Olá precisa toobe em uma **desativado** estado.
* Olá dispositivo de destino precisa tooshow backup como **pronto tooset backup** em Olá portal do Azure. Provisionar uma matriz de virtual de destino de saudação capacidade igual ou superior. Use tooconfigure de interface do usuário da web local hello e registrar com êxito a matriz de virtual de destino hello.
  
  > [!IMPORTANT]
  > Não tente tooconfigure Olá virtual dispositivo registrado por meio do serviço de saudação. Nenhuma configuração do dispositivo deve ser executada por meio do serviço de saudação.
  > 
  > 
* dispositivo de destino Olá não pode ter Olá mesmo nome como dispositivo de origem hello.
* dispositivo de origem e destino Hello ter toobe Olá mesmo tipo. Você só pode falhar em uma matriz virtual configurada como um servidor de arquivo de tooanother de servidor de arquivos. Olá mesmo é válido para um servidor do iSCSI.
* Para um servidor de arquivos da recuperação de desastres, recomendamos que você ingressar toohello de dispositivo de destino Olá mesmo domínio como origem de saudação. Essa configuração garante que as permissões de compartilhamento hello serão automaticamente resolvidas. Somente Olá failover tooa dispositivo de destino no hello mesmo domínio.
* dispositivos de destino disponíveis Olá para DR são Olá de dispositivos que têm o mesmo ou maior capacidade em comparação com o dispositivo de origem toohello. Olá dispositivos que estão conectado tooyour de serviço, mas não atendem Olá critérios de espaço em disco não estão disponíveis como dispositivos de destino.

### <a name="other-considerations"></a>Outras considerações

* Para um failover planejado 
  
  * É recomendável que você use todos os volumes de saudação ou compartilhamentos no dispositivo de origem Olá offline.
  * É recomendável que você faça um backup do dispositivo hello e continue com a perda de dados de toominimize Olá failover. 
* Um failover não planejado, dispositivo Olá usa hello mais recente backup toorestore Olá dados.

### <a name="device-failover-prechecks"></a>Verificações prévias de failover de dispositivo

Antes de Olá que DR começa, o dispositivo de Olá executa prechecks. Essas verificações ajudam a garantir que nenhum erro ocorra quando a recuperação de desastres começar. Olá prechecks incluem:

* Validação de conta de armazenamento hello.
* Verificando Olá tooAzure de conectividade de nuvem.
* Verificando o espaço disponível no dispositivo de destino hello.
* Verificando se um volume de dispositivo de origem de servidor iSCSI tem
  
  * nomes válidos de ACR.
  * IQN válido (que não exceda 220 caracteres).
  * senhas CHAP válidas (com 12 a 16 caracteres).

Se qualquer Olá anterior prechecks falhar, você não pode continuar com hello DR. Resolva esses problemas e tente realizar a recuperação de desastre novamente.

Depois Olá DR é concluída com êxito, Olá da propriedade de dados na nuvem no dispositivo de origem Olá Olá está transferidos toohello dispositivo de destino. dispositivo de origem Hello, em seguida, não está mais disponível no portal de saudação. Acessar os volumes/compartilhamentos tooall Olá no dispositivo de origem Olá será bloqueado e o dispositivo de destino Olá se tornar ativo.

> [!IMPORTANT]
> Embora Olá dispositivo não está mais disponível, máquina virtual Olá provisionado no sistema de host Olá ainda está consumindo recursos. Depois de saudação DR foi concluída com êxito, você pode excluir esta máquina virtual do seu sistema de host.
> 
> 

## <a name="fail-over-tooa-virtual-array"></a>O failover de matriz virtual tooa

É recomendável que você provisione, configure e registre outra Matriz Virtual StorSimple com o serviço Gerenciador de Dispositivos do StorSimple antes de executar este procedimento.

> [!IMPORTANT]
> 
> * Você não pode fazer o failover de um dispositivo virtual StorSimple 8000 series dispositivo tooa 1200.
> * Você pode fazer o failover de um dispositivo de FIPS não de tooa implantados no portal do governo hello ou um dispositivo do Federal Information Processing Standard (FIPS) habilitado dispositivo virtual tooanother FIPS habilitada.


Execute Olá seguindo as etapas toorestore Olá dispositivo tooa destino dispositivo virtual StorSimple.

1. Provisionar e configurar um dispositivo de destino que atenda Olá [pré-requisitos para failover de dispositivo](#prerequisites). Concluir configuração do dispositivo Olá por meio da interface do usuário da web local hello e registre-o serviço de Gerenciador de dispositivos de StorSimple tooyour. Se criar um servidor de arquivos, vá toostep 1 de [configurado como servidor de arquivos](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device). Se criar um servidor iSCSI, vá toostep 1 de [configurado como servidor iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).

2. Usar volumes/compartilhamento offline no host hello. tootake Olá volumes/compartilhamento off-line, consulte as instruções específicas do sistema operacional de toohello para host hello. Se não já offline, será necessário tootake todos os Olá volumes/compartilhamentos offline no dispositivo Olá Olá seguinte.
   
    1. Vá muito**dispositivos** folha e selecione seu dispositivo.
   
    2. Vá muito**Configurações > Gerenciar > compartilhamentos** (ou **Configurações > Gerenciar > Volumes**). 
   
    3. Selecione um compartilhamento/volume, clique com o botão direito do mouse e selecione **Colocar offline**. 
   
    4. Quando solicitado a confirmar, verifique **, entender o impacto de saudação de colocar esse compartilhamento offline.** 
   
    5. Clique em **Colocar offline**.

3. O serviço do Gerenciador de dispositivos de StorSimple, ir muito**gerenciamento > dispositivos**. Em Olá **dispositivos** folha, selecione e clique em seu dispositivo de origem.

4. Na folha do **painel Dispositivo**, clique em **Desativar**.

5. Em Olá **desativar** folha, você será solicitado para confirmação. A desativação do dispositivo é um processo *permanente* que não pode ser desfeito. Você também é tootake lembrado seus compartilhamentos/volumes offline no host de saudação. Digite hello tooconfirm de nome de dispositivo e clique em **desativar**.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover1.png)
6. a desativação Olá inicia. Após a desativação de saudação for concluída com êxito, você receberá uma notificação.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover2.png)
7. Na página de dispositivos hello, estado do dispositivo Olá agora será alterado muito**desativado**.
    ![](./media/storsimple-virtual-array-failover-dr/failover3.png)
8. Em Olá **dispositivos** folha, selecione e clique em dispositivo de origem desativadas Olá para failover. 
9. Em Olá **painel dispositivo** folha, clique em **failover**. 
10. Em Olá **failover dispositivo** folha, Olá a seguir:
    
    1. campo de dispositivo de origem Olá é preenchido automaticamente. Observe o tamanho total dos dados de saudação para o dispositivo de origem hello. tamanho dos dados Olá deve ser menor que a capacidade disponível Olá no dispositivo de destino hello. Examine os detalhes de saudação associados com o dispositivo de origem hello como nome do dispositivo, a capacidade total e nomes de saudação de compartilhamentos de saudação que fizeram failover.

    2. Na lista suspensa de saudação de dispositivos disponíveis, escolha um **dispositivo de destino**. Somente os dispositivos de saudação que possuem capacidade suficiente são exibidos na lista suspensa de saudação.

    3. Verifique se **entendo que esta operação falhará em um dispositivo de destino toohello dados**. 

    4. Clique em **Fazer failover**.
    
        ![](./media/storsimple-virtual-array-failover-dr/failover4.png)
11. Um trabalho de failover é iniciado e você recebe uma notificação. Vá muito**dispositivos > trabalhos** toomonitor Olá failover.
    
     ![](./media/storsimple-virtual-array-failover-dr/failover5.png)
12. Em Olá **trabalhos** folha, você vê um trabalho de failover criado para o dispositivo de origem hello. Este trabalho executa Olá DR prechecks.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover6.png)
    
     Depois de saudação DR prechecks forem bem-sucedidas, o trabalho de failover Olá irá gerar trabalhos de restauração para cada volume/compartilhamento que existe no seu dispositivo de origem.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover7.png)
13. Após failover Olá é concluída, vá toohello **dispositivos** folha.
    
    1. Selecione e clique em dispositivo StorSimple Olá que foi usado como dispositivo de destino Olá para o processo de failover hello.
    2. Vá muito**Configurações > Gerenciamento > compartilhamentos** (ou **Volumes** se o servidor iSCSI). Em Olá **compartilhamentos** folha, você pode exibir todos os compartilhamentos de saudação (volumes) do dispositivo antigo hello.
        ![](./media/storsimple-virtual-array-failover-dr/failover9.png)
14. Você precisará de muito[criar um alias DNS](https://support.microsoft.com/kb/168322) para que todos os aplicativos que estão tentando de Olá tooconnect pode obter toohello redirecionado novo dispositivo.

## <a name="errors-during-dr"></a>Erros durante a recuperação de desastre

**Falha de conectividade de nuvem durante a recuperação de desastre**

Se a conectividade de nuvem de saudação é interrompida após DR foi iniciado e antes de saudação dispositivo restauração for concluída, Olá DR falhará. Você receberá uma notificação de failover. dispositivo de destino Olá para recuperação de desastres é marcado como *inutilizável.* Você não pode usar o hello mesmo dispositivo de destino para futuras DRs.

**Nenhum dispositivo de destino compatível**

Se os dispositivos de destino disponíveis Olá não tem espaço suficiente, você verá um efeito de toohello de erro que não há nenhum dispositivo de destino compatível.

**Falhas de pré-verificações**

Se uma saudação prechecks não for atendida, consulte precheck falhas.

## <a name="business-continuity-disaster-recovery-bcdr"></a>BCDR (recuperação de desastre de continuidade de negócios)

Um cenário de recuperação (BCDR) de desastres de continuidade de negócios ocorre quando Olá data center inteiro do Azure para de funcionar. Isso pode afetar o serviço do Gerenciador de dispositivos do StorSimple e Olá associados dispositivos StorSimple.

Se não houver dispositivos StorSimple que foram registrados antes de um desastre ocorreu, em seguida, esses dispositivos StorSimple talvez seja necessário toobe excluído. Após o desastre hello, você pode recriar e configurar esses dispositivos.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre como muito[administrar sua matriz Virtual StorSimple usando a interface da web local Olá](storsimple-ova-web-ui-admin.md).

