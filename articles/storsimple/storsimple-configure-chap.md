---
title: "aaaConfigure CHAP para o dispositivo da série StorSimple 8000 | Microsoft Docs"
description: "Descreve como tooconfigure Olá Challenge Handshake Authentication Protocol (CHAP) em um dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="4e3b6-103">Configure o CHAP para seu dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="4e3b6-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="4e3b6-104">Este tutorial explica como tooconfigure CHAP para seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="4e3b6-105">procedimento de saudação detalhado neste artigo se aplica a 8000 série tooStorSimple, bem como dispositivos de StorSimple 1200.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-105">hello procedure detailed in this article applies tooStorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="4e3b6-106">CHAP significa Challenge Handshake Authentication Protocol.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="4e3b6-107">É um esquema de autenticação usado por servidores toovalidate Olá identidade de clientes remotos.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="4e3b6-108">verificação de saudação baseia-se em uma senha secreta ou compartilhada.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="4e3b6-109">O protocolo CHAP pode ser unidirecional ou bidirecional (mútuo).</span><span class="sxs-lookup"><span data-stu-id="4e3b6-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="4e3b6-110">O CHAP é unidirecional quando Olá destino autentica um iniciador.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-110">One-way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="4e3b6-111">CHAP mútuo ou reverso, no hello o outro lado, requer que o destino Olá autentique o iniciador de saudação e, em seguida, o iniciador Olá autentique o destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-111">Mutual or reverse CHAP, on hello other hand, requires that hello target authenticate hello initiator and then hello initiator authenticate hello target.</span></span> <span data-ttu-id="4e3b6-112">A autenticação do iniciador pode ser implementada sem a autenticação do destino.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="4e3b6-113">No entanto, a autenticação do destino pode ser implementada somente se a autenticação do iniciador também for implementada.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="4e3b6-114">Como melhor prática, recomendamos que você use a segurança CHAP tooenhance iSCSI.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="4e3b6-115">Tenha em mente que não há suporte para IPSEC no momento em dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="4e3b6-116">as configurações de CHAP Olá no dispositivo do StorSimple Olá podem ser configuradas no hello maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e3b6-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="4e3b6-117">Autenticação unidirecional ou de uma via</span><span class="sxs-lookup"><span data-stu-id="4e3b6-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="4e3b6-118">Autenticação inversa bidirecional ou mútua</span><span class="sxs-lookup"><span data-stu-id="4e3b6-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="4e3b6-119">Em cada um desses casos, o portal de saudação para dispositivo hello e Olá software do iniciador iSCSI precisa toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="4e3b6-120">Olá a etapas detalhadas para essa configuração são descritas em Olá tutorial a seguir.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="4e3b6-121">Autenticação unidirecional ou de uma via</span><span class="sxs-lookup"><span data-stu-id="4e3b6-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="4e3b6-122">Na autenticação unidirecional, o destino de saudação autentica o iniciador de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="4e3b6-123">Esta autenticação exige que você configure configurações do iniciador CHAP Olá no dispositivo do StorSimple hello e Olá software iSCSI no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="4e3b6-124">Olá procedimentos detalhados para seu dispositivo StorSimple e host do Windows são descritos a seguir.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="4e3b6-125">tooconfigure seu dispositivo para autenticação unidirecional</span><span class="sxs-lookup"><span data-stu-id="4e3b6-125">tooconfigure your device for one-way authentication</span></span>
1. <span data-ttu-id="4e3b6-126">Em Olá portal clássico do Azure, em Olá **dispositivos** , clique em Olá **configurar** guia.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-126">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![Iniciador CHAP](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="4e3b6-128">Role para baixo nesta página e em Olá **iniciador CHAP** seção:</span><span class="sxs-lookup"><span data-stu-id="4e3b6-128">Scroll down on this page, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="4e3b6-129">Forneça um nome de usuário para o iniciador CHAP.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="4e3b6-130">Forneça uma senha para o iniciador CHAP.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="4e3b6-131">nome de usuário CHAP Olá deve conter menos de 233 caracteres.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-131">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="4e3b6-132">senha CHAP de saudação deve ter entre 12 e 16 caracteres.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-132">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="4e3b6-133">Um nome de usuário ou a senha mais longo resultará em uma falha de autenticação no host do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-133">A longer user name or password will result in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="4e3b6-134">Confirme senha hello.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-134">Confirm hello password.</span></span>
3. <span data-ttu-id="4e3b6-135">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-135">Click **Save**.</span></span> <span data-ttu-id="4e3b6-136">Uma mensagem de confirmação será exibida.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="4e3b6-137">Clique em **Okey** toosave alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-137">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="4e3b6-138">servidor de host de autenticação unidirecional de tooconfigure no Windows hello</span><span class="sxs-lookup"><span data-stu-id="4e3b6-138">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="4e3b6-139">No servidor de host do Windows hello, inicie o iniciador iSCSI de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-139">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="4e3b6-140">Em Olá **propriedades do iniciador iSCSI** janela, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e3b6-140">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="4e3b6-141">Clique em Olá **descoberta** guia.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-141">Click hello **Discovery** tab.</span></span>
      
       ![Propriedades do Iniciador iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="4e3b6-143">Clique em **Descobrir Portal**.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="4e3b6-144">Em Olá **descobrir Portal de destino** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="4e3b6-144">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="4e3b6-145">Especifique o endereço IP de saudação do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-145">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="4e3b6-146">Clique em **Avançado**.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-146">Click **Advanced**.</span></span>
      
       ![Descobrir Portal de Destino](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="4e3b6-148">Em Olá **configurações avançadas** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="4e3b6-148">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="4e3b6-149">Selecione Olá **habilitar CHAP logon** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-149">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="4e3b6-150">Em Olá **nome** campo, o nome de usuário de saudação de fonte que você especificou para Olá iniciador do CHAP no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-150">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="4e3b6-151">Em Olá **segredo de destino** campo, uma senha de saudação de fonte que você especificou para Olá iniciador do CHAP no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-151">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="4e3b6-152">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-152">Click **OK**.</span></span>
      
       ![Configurações gerais avançadas](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="4e3b6-154">Em Olá **destinos** guia da saudação **propriedades do iniciador iSCSI** janela, o status do dispositivo Olá devem aparecer como **conectado**.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-154">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="4e3b6-155">Se você estiver usando um dispositivo StorSimple 1200, cada volume será montado como um destino iSCSI conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="4e3b6-156">Portanto, as etapas 3 a 4 precisará toobe repetido para cada volume.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-156">Hence, steps  3-4 will need toobe repeated for each volume.</span></span>
   
    ![Volumes montados como destinos separados](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="4e3b6-158">Se você alterar o nome do iSCSI Olá, nome novo da saudação será usado para novas sessões do iSCSI.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-158">If you change hello iSCSI name, hello new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="4e3b6-159">Novas configurações não são usadas para sessões existentes até que você faça logoff e logon novamente.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="4e3b6-160">Para obter mais informações sobre como configurar o CHAP no servidor de host do Windows hello, ir muito[considerações adicionais](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="4e3b6-160">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="4e3b6-161">Autenticação bidirecional ou mútua</span><span class="sxs-lookup"><span data-stu-id="4e3b6-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="4e3b6-162">Na autenticação bidirecional, destino Olá autentica o iniciador hello e, em seguida, o iniciador Olá autentica o destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-162">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="4e3b6-163">Isso requer configurações do iniciador do CHAP tooconfigure Olá Olá usuário, bem como Olá reverter as configurações de CHAP no dispositivo de saudação e de software iSCSI no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-163">This requires hello user tooconfigure hello CHAP initiator settings, as well as hello reverse CHAP settings on hello device and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="4e3b6-164">Olá procedimentos a seguir descrevem autenticação mútua do hello etapas tooconfigure no dispositivo de saudação e no host do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-164">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="4e3b6-165">tooconfigure seu dispositivo para autenticação mútua</span><span class="sxs-lookup"><span data-stu-id="4e3b6-165">tooconfigure your device for mutual authentication</span></span>
1. <span data-ttu-id="4e3b6-166">Em Olá portal clássico do Azure, em Olá **dispositivos** , clique em Olá **configurar** guia.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-166">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![Destino do CHAP](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="4e3b6-168">Role para baixo nesta página e em Olá **CHAP de destino** seção:</span><span class="sxs-lookup"><span data-stu-id="4e3b6-168">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="4e3b6-169">Forneça um **Nome de usuário de CHAP reverso** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="4e3b6-170">Forneça uma **Senha de CHAP reversa** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="4e3b6-171">Confirme senha hello.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-171">Confirm hello password.</span></span>
3. <span data-ttu-id="4e3b6-172">Em Olá **iniciador CHAP** seção:</span><span class="sxs-lookup"><span data-stu-id="4e3b6-172">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="4e3b6-173">Forneça um **nome de usuário** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="4e3b6-174">Forneça uma **senha** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="4e3b6-175">Confirme senha hello.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-175">Confirm hello password.</span></span>
4. <span data-ttu-id="4e3b6-176">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-176">Click **Save**.</span></span> <span data-ttu-id="4e3b6-177">Uma mensagem de confirmação será exibida.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="4e3b6-178">Clique em **Okey** toosave alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-178">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="4e3b6-179">servidor de host de tooconfigure bidirecional autenticação no Windows hello</span><span class="sxs-lookup"><span data-stu-id="4e3b6-179">tooconfigure bidirectional authentication on hello Windows host server</span></span>
1. <span data-ttu-id="4e3b6-180">No servidor de host do Windows hello, inicie o iniciador iSCSI de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-180">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="4e3b6-181">Em Olá **propriedades do iniciador iSCSI** janela, clique em Olá **configuração** guia.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-181">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="4e3b6-182">Clique em **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="4e3b6-183">Em Olá **segredo CHAP mútuo do iniciador de iSCSI** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="4e3b6-183">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="4e3b6-184">Saudação de tipo **senha do CHAP reverso** que você configurou no hello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-184">Type hello **Reverse CHAP Password** that you configured in hello Azure classic portal.</span></span>
   2. <span data-ttu-id="4e3b6-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-185">Click **OK**.</span></span>
      
       ![Segredo do CHAP Mútuo do Iniciador iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="4e3b6-187">Clique em Olá **destinos** guia.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-187">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="4e3b6-188">Clique em Olá **conectar** botão.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-188">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="4e3b6-189">Em Olá **conectar tooTarget** caixa de diálogo, clique em **avançado**.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-189">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="4e3b6-190">Em Olá **propriedades avançadas** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="4e3b6-190">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="4e3b6-191">Selecione Olá **habilitar CHAP logon** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-191">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="4e3b6-192">Em Olá **nome** campo, o nome de usuário de saudação de fonte que você especificou para Olá iniciador do CHAP no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-192">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="4e3b6-193">Em Olá **segredo de destino** campo, uma senha de saudação de fonte que você especificou para Olá iniciador do CHAP no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-193">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="4e3b6-194">Selecione Olá **realizar autenticação mútua** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-194">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Configurações avançadas de autenticação mútua](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="4e3b6-196">Clique em **Okey** configuração do CHAP Olá toocomplete</span><span class="sxs-lookup"><span data-stu-id="4e3b6-196">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="4e3b6-197">Para obter mais informações sobre como configurar o CHAP no servidor de host do Windows hello, ir muito[considerações adicionais](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="4e3b6-197">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="4e3b6-198">Considerações adicionais</span><span class="sxs-lookup"><span data-stu-id="4e3b6-198">Additional considerations</span></span>
<span data-ttu-id="4e3b6-199">Olá **conexão rápida** não oferece suporte a conexões que têm o CHAP habilitado.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-199">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="4e3b6-200">Quando o CHAP está habilitado, certifique-se de que você use Olá **conectar** botão está disponível em Olá **destinos** destino do guia tooconnect tooa.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-200">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Conecte-se tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="4e3b6-202">Em Olá **conectar tooTarget** caixa de diálogo que é apresentado, selecione hello **adicionar esta lista de toohello de conexão de destinos favoritos** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-202">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="4e3b6-203">Isso garante que sempre Olá computador for reiniciado, uma tentativa de destinos favoritos do iSCSI de toohello de conexão do toorestore hello.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-203">This ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="4e3b6-204">Erros durante a configuração</span><span class="sxs-lookup"><span data-stu-id="4e3b6-204">Errors during configuration</span></span>
<span data-ttu-id="4e3b6-205">Se a configuração do CHAP estiver incorreta, são provavelmente toosee um **falha de autenticação** mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-205">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="4e3b6-206">Verificação da configuração do CHAP</span><span class="sxs-lookup"><span data-stu-id="4e3b6-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="4e3b6-207">Você pode verificar que o CHAP está sendo usado por concluir Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-207">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="4e3b6-208">tooverify a configuração do CHAP</span><span class="sxs-lookup"><span data-stu-id="4e3b6-208">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="4e3b6-209">Clique em **Destinos Favoritos**.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="4e3b6-210">Selecione o destino Olá para o qual você habilitou a autenticação.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-210">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="4e3b6-211">Clique em **Detalhes**.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-211">Click **Details**.</span></span>
   
    ![Destinos favoritos das propriedades do Iniciador iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="4e3b6-213">Em Olá **detalhes do destino favorito** caixa de diálogo, observe entrada Olá Olá **autenticação** campo.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-213">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="4e3b6-214">Se a configuração de saudação foi bem-sucedida, ele deve indicar **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="4e3b6-214">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Detalhes do destino favorito](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="4e3b6-216">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4e3b6-216">Next steps</span></span>
* <span data-ttu-id="4e3b6-217">Saiba mais sobre a [segurança do StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="4e3b6-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="4e3b6-218">Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="4e3b6-218">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

