---
title: "Configurar o CHAP para o dispositivo StorSimple série 8000 | Microsoft Docs"
description: Descreve como configurar o CHAP (Challenge Handshake Authentication Protocol) em um dispositivo StorSimple.
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
ms.openlocfilehash: 36b4e73d0336deb9560d44163fc5330d1c9d775c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="c9e2e-103">Configure o CHAP para seu dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="c9e2e-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="c9e2e-104">Este tutorial explica como configurar o CHAP para seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-104">This tutorial explains how to configure CHAP for your StorSimple device.</span></span> <span data-ttu-id="c9e2e-105">O procedimento detalhado neste artigo se aplica ao StorSimple série 8000, bem como dispositivos StorSimple 1200.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-105">The procedure detailed in this article applies to StorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="c9e2e-106">CHAP significa Challenge Handshake Authentication Protocol.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="c9e2e-107">É um esquema de autenticação usado pelos servidores para validar a identidade de clientes remotos.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-107">It is an authentication scheme used by servers to validate the identity of remote clients.</span></span> <span data-ttu-id="c9e2e-108">A verificação baseia-se em uma senha ou segredo compartilhado.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-108">The verification is based on a shared password or secret.</span></span> <span data-ttu-id="c9e2e-109">O protocolo CHAP pode ser unidirecional ou bidirecional (mútuo).</span><span class="sxs-lookup"><span data-stu-id="c9e2e-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="c9e2e-110">O CHAP unidirecional é quando o destino autentica um iniciador.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-110">One-way CHAP is when the target authenticates an initiator.</span></span> <span data-ttu-id="c9e2e-111">CHAP mútuo ou inverso, por outro lado, requer que o destino autentique o iniciador e, em seguida, o iniciador autentique o destino.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-111">Mutual or reverse CHAP, on the other hand, requires that the target authenticate the initiator and then the initiator authenticate the target.</span></span> <span data-ttu-id="c9e2e-112">A autenticação do iniciador pode ser implementada sem a autenticação do destino.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="c9e2e-113">No entanto, a autenticação do destino pode ser implementada somente se a autenticação do iniciador também for implementada.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="c9e2e-114">Como prática recomendada, é sugerimos usar o CHAP para aumentar a segurança do iSCSI.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-114">As a best practice, we recommend that you use CHAP to enhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="c9e2e-115">Tenha em mente que não há suporte para IPSEC no momento em dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="c9e2e-116">As configurações do CHAP no dispositivo StorSimple podem ser definidas das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="c9e2e-116">The CHAP settings on the StorSimple device can be configured in the following ways:</span></span>

* <span data-ttu-id="c9e2e-117">Autenticação unidirecional ou de uma via</span><span class="sxs-lookup"><span data-stu-id="c9e2e-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="c9e2e-118">Autenticação inversa bidirecional ou mútua</span><span class="sxs-lookup"><span data-stu-id="c9e2e-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="c9e2e-119">Em cada um desses casos, o Portal para o dispositivo e o software do iniciador iSCSI do servidor precisam ser configurados.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-119">In each of these cases, the portal for the device and the server iSCSI initiator software needs to be configured.</span></span> <span data-ttu-id="c9e2e-120">O tutorial a seguir descreve as etapas detalhadas para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-120">The detailed steps for this configuration are described in the following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="c9e2e-121">Autenticação unidirecional ou de uma via</span><span class="sxs-lookup"><span data-stu-id="c9e2e-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="c9e2e-122">Na autenticação unidirecional, o destino autentica o iniciador.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-122">In unidirectional authentication, the target authenticates the initiator.</span></span> <span data-ttu-id="c9e2e-123">Essa autenticação exige que você defina as configurações do iniciador CHAP no dispositivo StorSimple e o software Iniciador iSCSI no host.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-123">This authentication requires that you configure the CHAP initiator settings on the StorSimple device and the iSCSI Initiator software on the host.</span></span> <span data-ttu-id="c9e2e-124">Os procedimentos detalhados para seu dispositivo StorSimple e o host do Windows são descritos a seguir.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-124">The detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="to-configure-your-device-for-one-way-authentication"></a><span data-ttu-id="c9e2e-125">Para configurar seu dispositivo para autenticação unidirecional</span><span class="sxs-lookup"><span data-stu-id="c9e2e-125">To configure your device for one-way authentication</span></span>
1. <span data-ttu-id="c9e2e-126">No Portal clássico do Azure, na página **Dispositivos**, clique na guia **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-126">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span></span>
   
    ![Iniciador CHAP](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="c9e2e-128">Role para baixo nesta página e, na seção **Iniciador CHAP** :</span><span class="sxs-lookup"><span data-stu-id="c9e2e-128">Scroll down on this page, and in the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="c9e2e-129">Forneça um nome de usuário para o iniciador CHAP.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="c9e2e-130">Forneça uma senha para o iniciador CHAP.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="c9e2e-131">O nome de usuário do CHAP deve conter menos de 233 caracteres.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-131">The CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="c9e2e-132">A senha do CHAP deve conter entre 12 e 16 caracteres.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-132">The CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="c9e2e-133">Um nome de usuário ou senha mais longo resultará em falha de autenticação no host do Windows.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-133">A longer user name or password will result in an authentication failure on the Windows host.</span></span>
   
   3. <span data-ttu-id="c9e2e-134">Confirme a senha.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-134">Confirm the password.</span></span>
3. <span data-ttu-id="c9e2e-135">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-135">Click **Save**.</span></span> <span data-ttu-id="c9e2e-136">Uma mensagem de confirmação será exibida.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="c9e2e-137">Clique em **OK** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-137">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-one-way-authentication-on-the-windows-host-server"></a><span data-ttu-id="c9e2e-138">Para configurar a autenticação unidirecional no servidor de host do Windows</span><span class="sxs-lookup"><span data-stu-id="c9e2e-138">To configure one-way authentication on the Windows host server</span></span>
1. <span data-ttu-id="c9e2e-139">No servidor de host do Windows, inicie o Iniciador iSCSI.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-139">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="c9e2e-140">Na janela **Propriedades do Iniciador iSCSI** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c9e2e-140">In the **iSCSI Initiator Properties** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="c9e2e-141">Clique na guia **Descoberta** .</span><span class="sxs-lookup"><span data-stu-id="c9e2e-141">Click the **Discovery** tab.</span></span>
      
       ![Propriedades do Iniciador iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="c9e2e-143">Clique em **Descobrir Portal**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="c9e2e-144">Na caixa de diálogo **Descobrir Portal de Destino** :</span><span class="sxs-lookup"><span data-stu-id="c9e2e-144">In the **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="c9e2e-145">Especifique o endereço IP do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-145">Specify the IP address of your device.</span></span>
   2. <span data-ttu-id="c9e2e-146">Clique em **Avançado**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-146">Click **Advanced**.</span></span>
      
       ![Descobrir Portal de Destino](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="c9e2e-148">Na caixa de diálogo **Configurações Avançadas** :</span><span class="sxs-lookup"><span data-stu-id="c9e2e-148">In the **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="c9e2e-149">Marque a caixa de seleção **Habilitar logon CHAP** .</span><span class="sxs-lookup"><span data-stu-id="c9e2e-149">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="c9e2e-150">No campo **Nome** , forneça o nome de usuário especificado para o Iniciador CHAP no Portal clássico.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-150">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="c9e2e-151">No campo **Segredo de destino** , forneça a senha especificada para o Iniciador CHAP no Portal clássico.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-151">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="c9e2e-152">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-152">Click **OK**.</span></span>
      
       ![Configurações gerais avançadas](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="c9e2e-154">Na guia **Destinos** da janela **Propriedades do Iniciador iSCSI**, o status do dispositivo deve aparecer como **Conectado**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-154">On the **Targets** tab of the **iSCSI Initiator Properties** window, the device status should appear as **Connected**.</span></span> <span data-ttu-id="c9e2e-155">Se você estiver usando um dispositivo StorSimple 1200, cada volume será montado como um destino iSCSI conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="c9e2e-156">Portanto, as etapas 3 a 4 precisarão ser repetidas para cada volume.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-156">Hence, steps  3-4 will need to be repeated for each volume.</span></span>
   
    ![Volumes montados como destinos separados](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="c9e2e-158">Se você alterar o nome iSCSI, o novo nome será usado para novas sessões do iSCSI.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-158">If you change the iSCSI name, the new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="c9e2e-159">Novas configurações não são usadas para sessões existentes até que você faça logoff e logon novamente.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="c9e2e-160">Para saber mais sobre como configurar o CHAP no servidor de host do Windows, vá para [Considerações adicionais](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="c9e2e-160">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="c9e2e-161">Autenticação bidirecional ou mútua</span><span class="sxs-lookup"><span data-stu-id="c9e2e-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="c9e2e-162">Na autenticação bidirecional, o destino autentica o iniciador e, em seguida, o iniciador autentica o destino.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-162">In bidirectional authentication, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="c9e2e-163">Isso exige que o usuário defina as configurações do iniciador CHAP, bem como as configurações de CHAP inversas no dispositivo e no software Iniciador iSCSI no host.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-163">This requires the user to configure the CHAP initiator settings, as well as the reverse CHAP settings on the device and iSCSI Initiator software on the host.</span></span> <span data-ttu-id="c9e2e-164">Os procedimentos a seguir descrevem as etapas para configurar a autenticação mútua no dispositivo e no host do Windows.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-164">The following procedures describe the steps to configure mutual authentication on the device and on the Windows host.</span></span>

#### <a name="to-configure-your-device-for-mutual-authentication"></a><span data-ttu-id="c9e2e-165">Para configurar seu dispositivo para autenticação mútua</span><span class="sxs-lookup"><span data-stu-id="c9e2e-165">To configure your device for mutual authentication</span></span>
1. <span data-ttu-id="c9e2e-166">No Portal clássico do Azure, na página **Dispositivos**, clique na guia **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-166">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span></span>
   
    ![Destino do CHAP](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="c9e2e-168">Role para baixo nessa página e, na seção **Destino do CHAP** :</span><span class="sxs-lookup"><span data-stu-id="c9e2e-168">Scroll down on this page, and in the **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="c9e2e-169">Forneça um **Nome de usuário de CHAP reverso** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="c9e2e-170">Forneça uma **Senha de CHAP reversa** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="c9e2e-171">Confirme a senha.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-171">Confirm the password.</span></span>
3. <span data-ttu-id="c9e2e-172">Na seção **Iniciador CHAP** :</span><span class="sxs-lookup"><span data-stu-id="c9e2e-172">In the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="c9e2e-173">Forneça um **nome de usuário** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="c9e2e-174">Forneça uma **senha** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="c9e2e-175">Confirme a senha.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-175">Confirm the password.</span></span>
4. <span data-ttu-id="c9e2e-176">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-176">Click **Save**.</span></span> <span data-ttu-id="c9e2e-177">Uma mensagem de confirmação será exibida.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="c9e2e-178">Clique em **OK** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-178">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-bidirectional-authentication-on-the-windows-host-server"></a><span data-ttu-id="c9e2e-179">Para configurar a autenticação bidirecional no servidor de host do Windows</span><span class="sxs-lookup"><span data-stu-id="c9e2e-179">To configure bidirectional authentication on the Windows host server</span></span>
1. <span data-ttu-id="c9e2e-180">No servidor de host do Windows, inicie o Iniciador iSCSI.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-180">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="c9e2e-181">Na janela **Propriedades do Iniciador iSCSI**, clique na guia **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-181">In the **iSCSI Initiator Properties** window, click the **Configuration** tab.</span></span>
3. <span data-ttu-id="c9e2e-182">Clique em **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="c9e2e-183">Na caixa de diálogo **Segredo do CHAP Mútuo do Iniciador iSCSI** :</span><span class="sxs-lookup"><span data-stu-id="c9e2e-183">In the **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="c9e2e-184">Digite a **Senha do CHAP Reversa** configurada no Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-184">Type the **Reverse CHAP Password** that you configured in the Azure classic portal.</span></span>
   2. <span data-ttu-id="c9e2e-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-185">Click **OK**.</span></span>
      
       ![Segredo do CHAP Mútuo do Iniciador iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="c9e2e-187">Clique na guia **Destinos** .</span><span class="sxs-lookup"><span data-stu-id="c9e2e-187">Click the **Targets** tab.</span></span>
6. <span data-ttu-id="c9e2e-188">Clique no botão **Conectar** .</span><span class="sxs-lookup"><span data-stu-id="c9e2e-188">Click the **Connect** button.</span></span> 
7. <span data-ttu-id="c9e2e-189">Na caixa de diálogo **Conectar ao Destino**, clique em **Avançado**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-189">In the **Connect To Target** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="c9e2e-190">Na caixa de diálogo **Propriedades Avançadas** :</span><span class="sxs-lookup"><span data-stu-id="c9e2e-190">In the **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="c9e2e-191">Marque a caixa de seleção **Habilitar logon CHAP** .</span><span class="sxs-lookup"><span data-stu-id="c9e2e-191">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="c9e2e-192">No campo **Nome** , forneça o nome de usuário especificado para o Iniciador CHAP no Portal clássico.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-192">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="c9e2e-193">No campo **Segredo de destino** , forneça a senha especificada para o Iniciador CHAP no Portal clássico.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-193">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="c9e2e-194">Marque a caixa de seleção **Executar a autenticação mútua** .</span><span class="sxs-lookup"><span data-stu-id="c9e2e-194">Select the **Perform mutual authentication** check box.</span></span>
      
       ![Configurações avançadas de autenticação mútua](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="c9e2e-196">Clique em **OK** para concluir a configuração CHAP</span><span class="sxs-lookup"><span data-stu-id="c9e2e-196">Click **OK** to complete the CHAP configuration</span></span>

<span data-ttu-id="c9e2e-197">Para saber mais sobre como configurar o CHAP no servidor de host do Windows, vá para [Considerações adicionais](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="c9e2e-197">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="c9e2e-198">Considerações adicionais</span><span class="sxs-lookup"><span data-stu-id="c9e2e-198">Additional considerations</span></span>
<span data-ttu-id="c9e2e-199">O recurso **Conexão Rápida** não dá suporte a conexões com o CHAP habilitado.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-199">The **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="c9e2e-200">Quando o CHAP estiver habilitado, use o botão **Conectar** disponível na guia **Destinos** para se conectar a um destino.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-200">When CHAP is enabled, make sure that you use the **Connect** button that is available on the **Targets** tab to connect to a target.</span></span>

![Conectar-se ao destino](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="c9e2e-202">Na caixa de diálogo **Conectar-se ao Destino** apresentada, marque a caixa de seleção **Adicionar esta conexão à lista de Destinos Favoritos**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-202">In the **Connect to Target** dialog box that is presented, select the **Add this connection to the list of Favorite Targets** check box.</span></span> <span data-ttu-id="c9e2e-203">Isso garante que sempre que o computador for reiniciado, seja feita uma tentativa de restaurar a conexão com os destinos favoritos do iSCSI.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-203">This ensures that every time the computer restarts, an attempt is made to restore the connection to the iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="c9e2e-204">Erros durante a configuração</span><span class="sxs-lookup"><span data-stu-id="c9e2e-204">Errors during configuration</span></span>
<span data-ttu-id="c9e2e-205">Se a sua configuração do CHAP estiver incorreta, provavelmente você verá uma mensagem de erro de **Falha na autenticação** .</span><span class="sxs-lookup"><span data-stu-id="c9e2e-205">If your CHAP configuration is incorrect, then you are likely to see an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="c9e2e-206">Verificação da configuração do CHAP</span><span class="sxs-lookup"><span data-stu-id="c9e2e-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="c9e2e-207">Você pode verificar se o CHAP está sendo usado executando as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-207">You can verify that CHAP is being used by completing the following steps.</span></span>

#### <a name="to-verify-your-chap-configuration"></a><span data-ttu-id="c9e2e-208">Para verificar a configuração do CHAP</span><span class="sxs-lookup"><span data-stu-id="c9e2e-208">To verify your CHAP configuration</span></span>
1. <span data-ttu-id="c9e2e-209">Clique em **Destinos Favoritos**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="c9e2e-210">Selecione o destino para o qual você habilitou a autenticação.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-210">Select the target for which you enabled authentication.</span></span>
3. <span data-ttu-id="c9e2e-211">Clique em **Detalhes**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-211">Click **Details**.</span></span>
   
    ![Destinos favoritos das propriedades do Iniciador iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="c9e2e-213">Na caixa de diálogo **Detalhes do Destino Favorito**, observe a entrada no campo **Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-213">In the **Favorite Target Details** dialog box, note the entry in the **Authentication** field.</span></span> <span data-ttu-id="c9e2e-214">Se a configuração for bem-sucedida, ela deverá dizer **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="c9e2e-214">If the configuration was successful, it should say **CHAP**.</span></span>
   
    ![Detalhes do destino favorito](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="c9e2e-216">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c9e2e-216">Next steps</span></span>
* <span data-ttu-id="c9e2e-217">Saiba mais sobre a [segurança do StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="c9e2e-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="c9e2e-218">Saiba mais sobre o [uso do serviço StorSimple Manager para administrar seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="c9e2e-218">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

