---
title: "aaaConfigure CHAP para o dispositivo da série StorSimple 8000 | Microsoft Docs"
description: "Descreve como tooconfigure Olá Challenge Handshake Authentication Protocol (CHAP) em um dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 3351184b0317da7e3deae398bc0d63c3e5bd930f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a>Configure o CHAP para seu dispositivo StorSimple

Este tutorial explica como tooconfigure CHAP para seu dispositivo StorSimple. procedimento de saudação detalhado neste artigo se aplica a dispositivos da série 8000 tooStorSimple.

CHAP significa Challenge Handshake Authentication Protocol. É um esquema de autenticação usado por servidores toovalidate Olá identidade de clientes remotos. verificação de saudação baseia-se em uma senha secreta ou compartilhada. O protocolo CHAP pode ter um sentido (unidirecional) ou sentido mútuo (bidirecional). Uma maneira CHAP é quando o destino de saudação autentica um iniciador. No CHAP mútuo ou reverso, destino Olá autentica o iniciador hello e, em seguida, o iniciador Olá autentica o destino de saudação. A autenticação do iniciador pode ser implementada sem a autenticação do destino. No entanto, a autenticação do destino pode ser implementada somente se a autenticação do iniciador também for implementada.

Como melhor prática, recomendamos que você use a segurança CHAP tooenhance iSCSI.

> [!NOTE]
> Tenha em mente que não há suporte para IPSEC no momento em dispositivos StorSimple.

as configurações de CHAP Olá no dispositivo do StorSimple Olá podem ser configuradas no hello maneiras a seguir:

* Autenticação unidirecional ou de uma via
* Autenticação inversa bidirecional ou mútua

Em cada um desses casos, o portal de saudação para dispositivo hello e Olá software do iniciador iSCSI precisa toobe configurado. Olá a etapas detalhadas para essa configuração são descritas em Olá tutorial a seguir.

## <a name="unidirectional-or-one-way-authentication"></a>Autenticação unidirecional ou de uma via

Na autenticação unidirecional, o destino de saudação autentica o iniciador de saudação. Esta autenticação exige que você configure configurações do iniciador CHAP Olá no dispositivo do StorSimple hello e Olá software iSCSI no host de saudação. Olá procedimentos detalhados para seu dispositivo StorSimple e host do Windows são descritos a seguir.

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a>tooconfigure seu dispositivo para autenticação unidirecional

1. No hello portal do Azure, vá tooyour serviço de Gerenciador de dispositivos do StorSimple. Clique em **dispositivos** e selecione e clique em um dispositivo que você deseja tooconfigure CHAP para. Vá muito**configurações do dispositivo > segurança**. Em Olá **as configurações de segurança** folha, clique em **CHAP**.
   
    ![Iniciador CHAP](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. Em Olá **CHAP** folha e em Olá **iniciador CHAP** seção:
   
   1. Forneça um nome de usuário para o iniciador CHAP.
   2. Forneça uma senha para o iniciador CHAP.
      
    > [!IMPORTANT]
    > nome de usuário CHAP Olá deve conter menos de 233 caracteres. senha CHAP de saudação deve ter entre 12 e 16 caracteres. Um nome de usuário ou a senha mais longo resulta em uma falha de autenticação no host do Windows hello.
   
   3. Confirme senha hello.

       ![Iniciador CHAP](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. Clique em **Salvar**. Uma mensagem de confirmação é exibida. Clique em **Okey** toosave alterações de saudação.

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a>servidor de host de autenticação unidirecional de tooconfigure no Windows hello
1. No servidor de host do Windows hello, inicie o iniciador iSCSI de saudação.
2. Em Olá **propriedades do iniciador iSCSI** janela, executar Olá etapas a seguir:
   
   1. Clique em Olá **descoberta** guia.
      
       ![Propriedades do Iniciador iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. Clique em **Descobrir Portal**.
3. Em Olá **descobrir Portal de destino** caixa de diálogo:
   
   1. Especifique o endereço IP de saudação do seu dispositivo.
   2. Clique em **Avançado**.
      
       ![Descobrir Portal de Destino](./media/storsimple-configure-chap/IC740945.png)
4. Em Olá **configurações avançadas** caixa de diálogo:
   
   1. Selecione Olá **habilitar CHAP logon** caixa de seleção.
   2. Em Olá **nome** campo, o nome de usuário de saudação de fonte que você especificou para Olá iniciador do CHAP no portal clássico do hello.
   3. Em Olá **segredo de destino** campo, uma senha de saudação de fonte que você especificou para Olá iniciador do CHAP no portal clássico do hello.
   4. Clique em **OK**.
      
       ![Configurações gerais avançadas](./media/storsimple-configure-chap/IC740946.png)
5. Em Olá **destinos** guia da saudação **propriedades do iniciador iSCSI** janela, o status do dispositivo Olá devem aparecer como **conectado**. Se você estiver usando um dispositivo StorSimple 1200, cada volume será montado como um destino iSCSI. Portanto, as etapas 3 a 4 precisará toobe repetido para cada volume.
   
    ![Volumes montados como destinos separados](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > Se você alterar o nome do iSCSI hello, Olá novo nome é usado para novas sessões do iSCSI. Novas configurações não são usadas para sessões existentes até que você faça logoff e logon novamente.

Para obter mais informações sobre como configurar o CHAP no servidor de host do Windows hello, ir muito[considerações adicionais](#additional-considerations).

## <a name="bidirectional-or-mutual-authentication"></a>Autenticação bidirecional ou mútua

Na autenticação bidirecional, destino Olá autentica o iniciador hello e, em seguida, o iniciador Olá autentica o destino de saudação. Este procedimento requer configurações do iniciador do CHAP Olá Olá usuário tooconfigure, reverter as configurações de CHAP no dispositivo hello e software iSCSI no host de saudação. Olá procedimentos a seguir descrevem autenticação mútua do hello etapas tooconfigure no dispositivo de saudação e no host do Windows hello.

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a>tooconfigure seu dispositivo para autenticação mútua

1. No hello portal do Azure, vá tooyour serviço de Gerenciador de dispositivos do StorSimple. Clique em **dispositivos** e selecione e clique em um dispositivo que você deseja tooconfigure CHAP para. Vá muito**configurações do dispositivo > segurança**. Em Olá **as configurações de segurança** folha, clique em **CHAP**.
   
    ![Destino do CHAP](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. Role para baixo nesta página e em Olá **CHAP de destino** seção:
   
   1. Forneça um **Nome de usuário de CHAP reverso** para seu dispositivo.
   2. Forneça uma **Senha de CHAP reversa** para seu dispositivo.
   3. Confirme senha hello.
3. Em Olá **iniciador CHAP** seção:
   
   1. Forneça um **nome de usuário** para seu dispositivo.
   2. Forneça uma **senha** para seu dispositivo.
   3. Confirme senha hello.

       ![Iniciador CHAP](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. Clique em **Salvar**. Uma mensagem de confirmação é exibida. Clique em **Okey** toosave alterações de saudação.

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a>servidor de host de tooconfigure bidirecional autenticação no Windows hello

1. No servidor de host do Windows hello, inicie o iniciador iSCSI de saudação.
2. Em Olá **propriedades do iniciador iSCSI** janela, clique em Olá **configuração** guia.
3. Clique em **CHAP**.
4. Em Olá **segredo CHAP mútuo do iniciador de iSCSI** caixa de diálogo:
   
   1. Saudação de tipo **senha do CHAP reverso** que você configurou no hello portal do Azure.
   2. Clique em **OK**.
      
       ![Segredo do CHAP Mútuo do Iniciador iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. Clique em Olá **destinos** guia.
6. Clique em Olá **conectar** botão. 
7. Em Olá **conectar tooTarget** caixa de diálogo, clique em **avançado**.
8. Em Olá **propriedades avançadas** caixa de diálogo:
   
   1. Selecione Olá **habilitar CHAP logon** caixa de seleção.
   2. Em Olá **nome** campo, o nome de usuário de saudação de fonte que você especificou para Olá iniciador do CHAP no portal clássico do hello.
   3. Em Olá **segredo de destino** campo, uma senha de saudação de fonte que você especificou para Olá iniciador do CHAP no portal clássico do hello.
   4. Selecione Olá **realizar autenticação mútua** caixa de seleção.
      
       ![Configurações avançadas de autenticação mútua](./media/storsimple-configure-chap/IC740950.png)
   5. Clique em **Okey** configuração do CHAP Olá toocomplete

Para obter mais informações sobre como configurar o CHAP no servidor de host do Windows hello, ir muito[considerações adicionais](#additional-considerations).

## <a name="additional-considerations"></a>Considerações adicionais

Olá **conexão rápida** não oferece suporte a conexões que têm o CHAP habilitado. Quando o CHAP está habilitado, certifique-se de que você use Olá **conectar** botão está disponível em Olá **destinos** destino do guia tooconnect tooa.

![Conecte-se tootarget](./media/storsimple-configure-chap/IC740947.png)

Em Olá **conectar tooTarget** caixa de diálogo que é apresentado, selecione hello **adicionar esta lista de toohello de conexão de destinos favoritos** caixa de seleção. Essa seleção garante que sempre Olá computador for reiniciado, uma tentativa de destinos favoritos do iSCSI de toohello de conexão do toorestore hello.

## <a name="errors-during-configuration"></a>Erros durante a configuração

Se a configuração do CHAP estiver incorreta, são provavelmente toosee um **falha de autenticação** mensagem de erro.

## <a name="verification-of-chap-configuration"></a>Verificação da configuração do CHAP

Você pode verificar que o CHAP está sendo usado por concluir Olá etapas a seguir.

#### <a name="tooverify-your-chap-configuration"></a>tooverify a configuração do CHAP
1. Clique em **Destinos Favoritos**.
2. Selecione o destino Olá para o qual você habilitou a autenticação.
3. Clique em **Detalhes**.
   
    ![Destinos favoritos das propriedades do Iniciador iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. Em Olá **detalhes do destino favorito** caixa de diálogo, observe entrada Olá Olá **autenticação** campo. Se a configuração de saudação foi bem-sucedida, ele deve indicar **CHAP**.
   
    ![Detalhes do destino favorito](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a>Próximas etapas

* Saiba mais sobre a [segurança do StorSimple](storsimple-8000-security.md).
* Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador de dispositivos do StorSimple em seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

