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
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="7a78f-103">Configure o CHAP para seu dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="7a78f-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="7a78f-104">Este tutorial explica como tooconfigure CHAP para seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7a78f-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="7a78f-105">procedimento de saudação detalhado neste artigo se aplica a dispositivos da série 8000 tooStorSimple.</span><span class="sxs-lookup"><span data-stu-id="7a78f-105">hello procedure detailed in this article applies tooStorSimple 8000 series devices.</span></span>

<span data-ttu-id="7a78f-106">CHAP significa Challenge Handshake Authentication Protocol.</span><span class="sxs-lookup"><span data-stu-id="7a78f-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="7a78f-107">É um esquema de autenticação usado por servidores toovalidate Olá identidade de clientes remotos.</span><span class="sxs-lookup"><span data-stu-id="7a78f-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="7a78f-108">verificação de saudação baseia-se em uma senha secreta ou compartilhada.</span><span class="sxs-lookup"><span data-stu-id="7a78f-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="7a78f-109">O protocolo CHAP pode ter um sentido (unidirecional) ou sentido mútuo (bidirecional).</span><span class="sxs-lookup"><span data-stu-id="7a78f-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="7a78f-110">Uma maneira CHAP é quando o destino de saudação autentica um iniciador.</span><span class="sxs-lookup"><span data-stu-id="7a78f-110">One way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="7a78f-111">No CHAP mútuo ou reverso, destino Olá autentica o iniciador hello e, em seguida, o iniciador Olá autentica o destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a78f-111">In mutual or reverse CHAP, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="7a78f-112">A autenticação do iniciador pode ser implementada sem a autenticação do destino.</span><span class="sxs-lookup"><span data-stu-id="7a78f-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="7a78f-113">No entanto, a autenticação do destino pode ser implementada somente se a autenticação do iniciador também for implementada.</span><span class="sxs-lookup"><span data-stu-id="7a78f-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="7a78f-114">Como melhor prática, recomendamos que você use a segurança CHAP tooenhance iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7a78f-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="7a78f-115">Tenha em mente que não há suporte para IPSEC no momento em dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7a78f-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="7a78f-116">as configurações de CHAP Olá no dispositivo do StorSimple Olá podem ser configuradas no hello maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a78f-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="7a78f-117">Autenticação unidirecional ou de uma via</span><span class="sxs-lookup"><span data-stu-id="7a78f-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="7a78f-118">Autenticação inversa bidirecional ou mútua</span><span class="sxs-lookup"><span data-stu-id="7a78f-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="7a78f-119">Em cada um desses casos, o portal de saudação para dispositivo hello e Olá software do iniciador iSCSI precisa toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="7a78f-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="7a78f-120">Olá a etapas detalhadas para essa configuração são descritas em Olá tutorial a seguir.</span><span class="sxs-lookup"><span data-stu-id="7a78f-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="7a78f-121">Autenticação unidirecional ou de uma via</span><span class="sxs-lookup"><span data-stu-id="7a78f-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="7a78f-122">Na autenticação unidirecional, o destino de saudação autentica o iniciador de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a78f-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="7a78f-123">Esta autenticação exige que você configure configurações do iniciador CHAP Olá no dispositivo do StorSimple hello e Olá software iSCSI no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a78f-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="7a78f-124">Olá procedimentos detalhados para seu dispositivo StorSimple e host do Windows são descritos a seguir.</span><span class="sxs-lookup"><span data-stu-id="7a78f-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="7a78f-125">tooconfigure seu dispositivo para autenticação unidirecional</span><span class="sxs-lookup"><span data-stu-id="7a78f-125">tooconfigure your device for one-way authentication</span></span>

1. <span data-ttu-id="7a78f-126">No hello portal do Azure, vá tooyour serviço de Gerenciador de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7a78f-126">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="7a78f-127">Clique em **dispositivos** e selecione e clique em um dispositivo que você deseja tooconfigure CHAP para.</span><span class="sxs-lookup"><span data-stu-id="7a78f-127">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="7a78f-128">Vá muito**configurações do dispositivo > segurança**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-128">Go too**Device settings > Security**.</span></span> <span data-ttu-id="7a78f-129">Em Olá **as configurações de segurança** folha, clique em **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-129">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![Iniciador CHAP](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="7a78f-131">Em Olá **CHAP** folha e em Olá **iniciador CHAP** seção:</span><span class="sxs-lookup"><span data-stu-id="7a78f-131">In hello **CHAP** blade, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="7a78f-132">Forneça um nome de usuário para o iniciador CHAP.</span><span class="sxs-lookup"><span data-stu-id="7a78f-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="7a78f-133">Forneça uma senha para o iniciador CHAP.</span><span class="sxs-lookup"><span data-stu-id="7a78f-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="7a78f-134">nome de usuário CHAP Olá deve conter menos de 233 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7a78f-134">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="7a78f-135">senha CHAP de saudação deve ter entre 12 e 16 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7a78f-135">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="7a78f-136">Um nome de usuário ou a senha mais longo resulta em uma falha de autenticação no host do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="7a78f-136">A longer user name or password results in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="7a78f-137">Confirme senha hello.</span><span class="sxs-lookup"><span data-stu-id="7a78f-137">Confirm hello password.</span></span>

       ![Iniciador CHAP](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="7a78f-139">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-139">Click **Save**.</span></span> <span data-ttu-id="7a78f-140">Uma mensagem de confirmação é exibida.</span><span class="sxs-lookup"><span data-stu-id="7a78f-140">A confirmation message is displayed.</span></span> <span data-ttu-id="7a78f-141">Clique em **Okey** toosave alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a78f-141">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="7a78f-142">servidor de host de autenticação unidirecional de tooconfigure no Windows hello</span><span class="sxs-lookup"><span data-stu-id="7a78f-142">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="7a78f-143">No servidor de host do Windows hello, inicie o iniciador iSCSI de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a78f-143">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="7a78f-144">Em Olá **propriedades do iniciador iSCSI** janela, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a78f-144">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="7a78f-145">Clique em Olá **descoberta** guia.</span><span class="sxs-lookup"><span data-stu-id="7a78f-145">Click hello **Discovery** tab.</span></span>
      
       ![Propriedades do Iniciador iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="7a78f-147">Clique em **Descobrir Portal**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="7a78f-148">Em Olá **descobrir Portal de destino** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="7a78f-148">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="7a78f-149">Especifique o endereço IP de saudação do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7a78f-149">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="7a78f-150">Clique em **Avançado**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-150">Click **Advanced**.</span></span>
      
       ![Descobrir Portal de Destino](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="7a78f-152">Em Olá **configurações avançadas** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="7a78f-152">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="7a78f-153">Selecione Olá **habilitar CHAP logon** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="7a78f-153">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="7a78f-154">Em Olá **nome** campo, o nome de usuário de saudação de fonte que você especificou para Olá iniciador do CHAP no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="7a78f-154">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="7a78f-155">Em Olá **segredo de destino** campo, uma senha de saudação de fonte que você especificou para Olá iniciador do CHAP no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="7a78f-155">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="7a78f-156">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-156">Click **OK**.</span></span>
      
       ![Configurações gerais avançadas](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="7a78f-158">Em Olá **destinos** guia da saudação **propriedades do iniciador iSCSI** janela, o status do dispositivo Olá devem aparecer como **conectado**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-158">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="7a78f-159">Se você estiver usando um dispositivo StorSimple 1200, cada volume será montado como um destino iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7a78f-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="7a78f-160">Portanto, as etapas 3 a 4 precisará toobe repetido para cada volume.</span><span class="sxs-lookup"><span data-stu-id="7a78f-160">Hence, steps 3-4 will need toobe repeated for each volume.</span></span>
   
    ![Volumes montados como destinos separados](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="7a78f-162">Se você alterar o nome do iSCSI hello, Olá novo nome é usado para novas sessões do iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7a78f-162">If you change hello iSCSI name, hello new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="7a78f-163">Novas configurações não são usadas para sessões existentes até que você faça logoff e logon novamente.</span><span class="sxs-lookup"><span data-stu-id="7a78f-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="7a78f-164">Para obter mais informações sobre como configurar o CHAP no servidor de host do Windows hello, ir muito[considerações adicionais](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="7a78f-164">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="7a78f-165">Autenticação bidirecional ou mútua</span><span class="sxs-lookup"><span data-stu-id="7a78f-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="7a78f-166">Na autenticação bidirecional, destino Olá autentica o iniciador hello e, em seguida, o iniciador Olá autentica o destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a78f-166">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="7a78f-167">Este procedimento requer configurações do iniciador do CHAP Olá Olá usuário tooconfigure, reverter as configurações de CHAP no dispositivo hello e software iSCSI no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a78f-167">This procedure requires hello user tooconfigure hello CHAP initiator settings, reverse CHAP settings on hello device, and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="7a78f-168">Olá procedimentos a seguir descrevem autenticação mútua do hello etapas tooconfigure no dispositivo de saudação e no host do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="7a78f-168">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="7a78f-169">tooconfigure seu dispositivo para autenticação mútua</span><span class="sxs-lookup"><span data-stu-id="7a78f-169">tooconfigure your device for mutual authentication</span></span>

1. <span data-ttu-id="7a78f-170">No hello portal do Azure, vá tooyour serviço de Gerenciador de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7a78f-170">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="7a78f-171">Clique em **dispositivos** e selecione e clique em um dispositivo que você deseja tooconfigure CHAP para.</span><span class="sxs-lookup"><span data-stu-id="7a78f-171">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="7a78f-172">Vá muito**configurações do dispositivo > segurança**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-172">Go too**Device settings > Security**.</span></span> <span data-ttu-id="7a78f-173">Em Olá **as configurações de segurança** folha, clique em **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-173">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![Destino do CHAP](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="7a78f-175">Role para baixo nesta página e em Olá **CHAP de destino** seção:</span><span class="sxs-lookup"><span data-stu-id="7a78f-175">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="7a78f-176">Forneça um **Nome de usuário de CHAP reverso** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7a78f-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="7a78f-177">Forneça uma **Senha de CHAP reversa** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7a78f-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="7a78f-178">Confirme senha hello.</span><span class="sxs-lookup"><span data-stu-id="7a78f-178">Confirm hello password.</span></span>
3. <span data-ttu-id="7a78f-179">Em Olá **iniciador CHAP** seção:</span><span class="sxs-lookup"><span data-stu-id="7a78f-179">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="7a78f-180">Forneça um **nome de usuário** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7a78f-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="7a78f-181">Forneça uma **senha** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7a78f-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="7a78f-182">Confirme senha hello.</span><span class="sxs-lookup"><span data-stu-id="7a78f-182">Confirm hello password.</span></span>

       ![Iniciador CHAP](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="7a78f-184">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-184">Click **Save**.</span></span> <span data-ttu-id="7a78f-185">Uma mensagem de confirmação é exibida.</span><span class="sxs-lookup"><span data-stu-id="7a78f-185">A confirmation message is displayed.</span></span> <span data-ttu-id="7a78f-186">Clique em **Okey** toosave alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a78f-186">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="7a78f-187">servidor de host de tooconfigure bidirecional autenticação no Windows hello</span><span class="sxs-lookup"><span data-stu-id="7a78f-187">tooconfigure bidirectional authentication on hello Windows host server</span></span>

1. <span data-ttu-id="7a78f-188">No servidor de host do Windows hello, inicie o iniciador iSCSI de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a78f-188">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="7a78f-189">Em Olá **propriedades do iniciador iSCSI** janela, clique em Olá **configuração** guia.</span><span class="sxs-lookup"><span data-stu-id="7a78f-189">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="7a78f-190">Clique em **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="7a78f-191">Em Olá **segredo CHAP mútuo do iniciador de iSCSI** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="7a78f-191">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="7a78f-192">Saudação de tipo **senha do CHAP reverso** que você configurou no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a78f-192">Type hello **Reverse CHAP Password** that you configured in hello Azure portal.</span></span>
   2. <span data-ttu-id="7a78f-193">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-193">Click **OK**.</span></span>
      
       ![Segredo do CHAP Mútuo do Iniciador iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="7a78f-195">Clique em Olá **destinos** guia.</span><span class="sxs-lookup"><span data-stu-id="7a78f-195">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="7a78f-196">Clique em Olá **conectar** botão.</span><span class="sxs-lookup"><span data-stu-id="7a78f-196">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="7a78f-197">Em Olá **conectar tooTarget** caixa de diálogo, clique em **avançado**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-197">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="7a78f-198">Em Olá **propriedades avançadas** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="7a78f-198">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="7a78f-199">Selecione Olá **habilitar CHAP logon** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="7a78f-199">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="7a78f-200">Em Olá **nome** campo, o nome de usuário de saudação de fonte que você especificou para Olá iniciador do CHAP no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="7a78f-200">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="7a78f-201">Em Olá **segredo de destino** campo, uma senha de saudação de fonte que você especificou para Olá iniciador do CHAP no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="7a78f-201">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="7a78f-202">Selecione Olá **realizar autenticação mútua** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="7a78f-202">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Configurações avançadas de autenticação mútua](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="7a78f-204">Clique em **Okey** configuração do CHAP Olá toocomplete</span><span class="sxs-lookup"><span data-stu-id="7a78f-204">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="7a78f-205">Para obter mais informações sobre como configurar o CHAP no servidor de host do Windows hello, ir muito[considerações adicionais](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="7a78f-205">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="7a78f-206">Considerações adicionais</span><span class="sxs-lookup"><span data-stu-id="7a78f-206">Additional considerations</span></span>

<span data-ttu-id="7a78f-207">Olá **conexão rápida** não oferece suporte a conexões que têm o CHAP habilitado.</span><span class="sxs-lookup"><span data-stu-id="7a78f-207">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="7a78f-208">Quando o CHAP está habilitado, certifique-se de que você use Olá **conectar** botão está disponível em Olá **destinos** destino do guia tooconnect tooa.</span><span class="sxs-lookup"><span data-stu-id="7a78f-208">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Conecte-se tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="7a78f-210">Em Olá **conectar tooTarget** caixa de diálogo que é apresentado, selecione hello **adicionar esta lista de toohello de conexão de destinos favoritos** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="7a78f-210">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="7a78f-211">Essa seleção garante que sempre Olá computador for reiniciado, uma tentativa de destinos favoritos do iSCSI de toohello de conexão do toorestore hello.</span><span class="sxs-lookup"><span data-stu-id="7a78f-211">This selection ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="7a78f-212">Erros durante a configuração</span><span class="sxs-lookup"><span data-stu-id="7a78f-212">Errors during configuration</span></span>

<span data-ttu-id="7a78f-213">Se a configuração do CHAP estiver incorreta, são provavelmente toosee um **falha de autenticação** mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="7a78f-213">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="7a78f-214">Verificação da configuração do CHAP</span><span class="sxs-lookup"><span data-stu-id="7a78f-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="7a78f-215">Você pode verificar que o CHAP está sendo usado por concluir Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="7a78f-215">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="7a78f-216">tooverify a configuração do CHAP</span><span class="sxs-lookup"><span data-stu-id="7a78f-216">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="7a78f-217">Clique em **Destinos Favoritos**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="7a78f-218">Selecione o destino Olá para o qual você habilitou a autenticação.</span><span class="sxs-lookup"><span data-stu-id="7a78f-218">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="7a78f-219">Clique em **Detalhes**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-219">Click **Details**.</span></span>
   
    ![Destinos favoritos das propriedades do Iniciador iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="7a78f-221">Em Olá **detalhes do destino favorito** caixa de diálogo, observe entrada Olá Olá **autenticação** campo.</span><span class="sxs-lookup"><span data-stu-id="7a78f-221">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="7a78f-222">Se a configuração de saudação foi bem-sucedida, ele deve indicar **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="7a78f-222">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Detalhes do destino favorito](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="7a78f-224">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7a78f-224">Next steps</span></span>

* <span data-ttu-id="7a78f-225">Saiba mais sobre a [segurança do StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="7a78f-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="7a78f-226">Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador de dispositivos do StorSimple em seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="7a78f-226">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

