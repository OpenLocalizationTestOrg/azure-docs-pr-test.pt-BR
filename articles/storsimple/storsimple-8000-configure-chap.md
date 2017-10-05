---
title: "Configurar o CHAP para o dispositivo StorSimple série 8000 | Microsoft Docs"
description: Descreve como configurar o CHAP (Challenge Handshake Authentication Protocol) em um dispositivo StorSimple.
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
ms.openlocfilehash: 61e0877187759d76b6f7efcef0a5ed8bec8500fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="9177c-103">Configure o CHAP para seu dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="9177c-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="9177c-104">Este tutorial explica como configurar o CHAP para seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9177c-104">This tutorial explains how to configure CHAP for your StorSimple device.</span></span> <span data-ttu-id="9177c-105">O procedimento detalhado neste artigo aplica-se aos dispositivos StorSimple da série 8000.</span><span class="sxs-lookup"><span data-stu-id="9177c-105">The procedure detailed in this article applies to StorSimple 8000 series devices.</span></span>

<span data-ttu-id="9177c-106">CHAP significa Challenge Handshake Authentication Protocol.</span><span class="sxs-lookup"><span data-stu-id="9177c-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="9177c-107">É um esquema de autenticação usado pelos servidores para validar a identidade de clientes remotos.</span><span class="sxs-lookup"><span data-stu-id="9177c-107">It is an authentication scheme used by servers to validate the identity of remote clients.</span></span> <span data-ttu-id="9177c-108">A verificação baseia-se em uma senha ou segredo compartilhado.</span><span class="sxs-lookup"><span data-stu-id="9177c-108">The verification is based on a shared password or secret.</span></span> <span data-ttu-id="9177c-109">O protocolo CHAP pode ter um sentido (unidirecional) ou sentido mútuo (bidirecional).</span><span class="sxs-lookup"><span data-stu-id="9177c-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="9177c-110">O CHAP unidirecional é quando o destino autentica um iniciador.</span><span class="sxs-lookup"><span data-stu-id="9177c-110">One way CHAP is when the target authenticates an initiator.</span></span> <span data-ttu-id="9177c-111">No CHAP mútuo ou inverso, o destino autentica o iniciador e, em seguida, o iniciador autentica o destino.</span><span class="sxs-lookup"><span data-stu-id="9177c-111">In mutual or reverse CHAP, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="9177c-112">A autenticação do iniciador pode ser implementada sem a autenticação do destino.</span><span class="sxs-lookup"><span data-stu-id="9177c-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="9177c-113">No entanto, a autenticação do destino pode ser implementada somente se a autenticação do iniciador também for implementada.</span><span class="sxs-lookup"><span data-stu-id="9177c-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="9177c-114">Como prática recomendada, é sugerimos usar o CHAP para aumentar a segurança do iSCSI.</span><span class="sxs-lookup"><span data-stu-id="9177c-114">As a best practice, we recommend that you use CHAP to enhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="9177c-115">Tenha em mente que não há suporte para IPSEC no momento em dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9177c-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="9177c-116">As configurações do CHAP no dispositivo StorSimple podem ser definidas das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="9177c-116">The CHAP settings on the StorSimple device can be configured in the following ways:</span></span>

* <span data-ttu-id="9177c-117">Autenticação unidirecional ou de uma via</span><span class="sxs-lookup"><span data-stu-id="9177c-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="9177c-118">Autenticação inversa bidirecional ou mútua</span><span class="sxs-lookup"><span data-stu-id="9177c-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="9177c-119">Em cada um desses casos, o Portal para o dispositivo e o software do iniciador iSCSI do servidor precisam ser configurados.</span><span class="sxs-lookup"><span data-stu-id="9177c-119">In each of these cases, the portal for the device and the server iSCSI initiator software needs to be configured.</span></span> <span data-ttu-id="9177c-120">O tutorial a seguir descreve as etapas detalhadas para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="9177c-120">The detailed steps for this configuration are described in the following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="9177c-121">Autenticação unidirecional ou de uma via</span><span class="sxs-lookup"><span data-stu-id="9177c-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="9177c-122">Na autenticação unidirecional, o destino autentica o iniciador.</span><span class="sxs-lookup"><span data-stu-id="9177c-122">In unidirectional authentication, the target authenticates the initiator.</span></span> <span data-ttu-id="9177c-123">Essa autenticação exige que você defina as configurações do iniciador CHAP no dispositivo StorSimple e o software Iniciador iSCSI no host.</span><span class="sxs-lookup"><span data-stu-id="9177c-123">This authentication requires that you configure the CHAP initiator settings on the StorSimple device and the iSCSI Initiator software on the host.</span></span> <span data-ttu-id="9177c-124">Os procedimentos detalhados para seu dispositivo StorSimple e o host do Windows são descritos a seguir.</span><span class="sxs-lookup"><span data-stu-id="9177c-124">The detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="to-configure-your-device-for-one-way-authentication"></a><span data-ttu-id="9177c-125">Para configurar seu dispositivo para autenticação unidirecional</span><span class="sxs-lookup"><span data-stu-id="9177c-125">To configure your device for one-way authentication</span></span>

1. <span data-ttu-id="9177c-126">No Portal do Azure, acesse seu serviço do Gerenciador de Dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9177c-126">In the Azure portal, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="9177c-127">Clique em **Dispositivos** e selecione e clique em um dispositivo para o qual você deseja configurar o CHAP.</span><span class="sxs-lookup"><span data-stu-id="9177c-127">Click **Devices** and select and click a device you wish to configure CHAP for.</span></span> <span data-ttu-id="9177c-128">Acesse **Configurações do dispositivo > Segurança**.</span><span class="sxs-lookup"><span data-stu-id="9177c-128">Go to **Device settings > Security**.</span></span> <span data-ttu-id="9177c-129">Na folha **Configurações de segurança**, clique em **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="9177c-129">In the **Security settings** blade, click **CHAP**.</span></span>
   
    ![Iniciador CHAP](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="9177c-131">Na folha **CHAP** e na seção **Iniciador CHAP**:</span><span class="sxs-lookup"><span data-stu-id="9177c-131">In the **CHAP** blade, and in the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="9177c-132">Forneça um nome de usuário para o iniciador CHAP.</span><span class="sxs-lookup"><span data-stu-id="9177c-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="9177c-133">Forneça uma senha para o iniciador CHAP.</span><span class="sxs-lookup"><span data-stu-id="9177c-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="9177c-134">O nome de usuário do CHAP deve conter menos de 233 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9177c-134">The CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="9177c-135">A senha do CHAP deve conter entre 12 e 16 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9177c-135">The CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="9177c-136">Um nome de usuário ou senha mais longo resultará em uma falha de autenticação no host do Windows.</span><span class="sxs-lookup"><span data-stu-id="9177c-136">A longer user name or password results in an authentication failure on the Windows host.</span></span>
   
   3. <span data-ttu-id="9177c-137">Confirme a senha.</span><span class="sxs-lookup"><span data-stu-id="9177c-137">Confirm the password.</span></span>

       ![Iniciador CHAP](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="9177c-139">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9177c-139">Click **Save**.</span></span> <span data-ttu-id="9177c-140">Uma mensagem de confirmação é exibida.</span><span class="sxs-lookup"><span data-stu-id="9177c-140">A confirmation message is displayed.</span></span> <span data-ttu-id="9177c-141">Clique em **OK** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="9177c-141">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-one-way-authentication-on-the-windows-host-server"></a><span data-ttu-id="9177c-142">Para configurar a autenticação unidirecional no servidor de host do Windows</span><span class="sxs-lookup"><span data-stu-id="9177c-142">To configure one-way authentication on the Windows host server</span></span>
1. <span data-ttu-id="9177c-143">No servidor de host do Windows, inicie o Iniciador iSCSI.</span><span class="sxs-lookup"><span data-stu-id="9177c-143">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="9177c-144">Na janela **Propriedades do Iniciador iSCSI** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9177c-144">In the **iSCSI Initiator Properties** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="9177c-145">Clique na guia **Descoberta** .</span><span class="sxs-lookup"><span data-stu-id="9177c-145">Click the **Discovery** tab.</span></span>
      
       ![Propriedades do Iniciador iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="9177c-147">Clique em **Descobrir Portal**.</span><span class="sxs-lookup"><span data-stu-id="9177c-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="9177c-148">Na caixa de diálogo **Descobrir Portal de Destino** :</span><span class="sxs-lookup"><span data-stu-id="9177c-148">In the **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="9177c-149">Especifique o endereço IP do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9177c-149">Specify the IP address of your device.</span></span>
   2. <span data-ttu-id="9177c-150">Clique em **Avançado**.</span><span class="sxs-lookup"><span data-stu-id="9177c-150">Click **Advanced**.</span></span>
      
       ![Descobrir Portal de Destino](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="9177c-152">Na caixa de diálogo **Configurações Avançadas** :</span><span class="sxs-lookup"><span data-stu-id="9177c-152">In the **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="9177c-153">Marque a caixa de seleção **Habilitar logon CHAP** .</span><span class="sxs-lookup"><span data-stu-id="9177c-153">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="9177c-154">No campo **Nome** , forneça o nome de usuário especificado para o Iniciador CHAP no Portal clássico.</span><span class="sxs-lookup"><span data-stu-id="9177c-154">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="9177c-155">No campo **Segredo de destino** , forneça a senha especificada para o Iniciador CHAP no Portal clássico.</span><span class="sxs-lookup"><span data-stu-id="9177c-155">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="9177c-156">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9177c-156">Click **OK**.</span></span>
      
       ![Configurações gerais avançadas](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="9177c-158">Na guia **Destinos** da janela **Propriedades do Iniciador iSCSI**, o status do dispositivo deve aparecer como **Conectado**.</span><span class="sxs-lookup"><span data-stu-id="9177c-158">On the **Targets** tab of the **iSCSI Initiator Properties** window, the device status should appear as **Connected**.</span></span> <span data-ttu-id="9177c-159">Se você estiver usando um dispositivo StorSimple 1200, cada volume será montado como um destino iSCSI.</span><span class="sxs-lookup"><span data-stu-id="9177c-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="9177c-160">Portanto, as etapas 3 a 4 precisarão ser repetidas para cada volume.</span><span class="sxs-lookup"><span data-stu-id="9177c-160">Hence, steps 3-4 will need to be repeated for each volume.</span></span>
   
    ![Volumes montados como destinos separados](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="9177c-162">Se você alterar o nome iSCSI, o novo nome será usado para novas sessões do iSCSI.</span><span class="sxs-lookup"><span data-stu-id="9177c-162">If you change the iSCSI name, the new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="9177c-163">Novas configurações não são usadas para sessões existentes até que você faça logoff e logon novamente.</span><span class="sxs-lookup"><span data-stu-id="9177c-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="9177c-164">Para saber mais sobre como configurar o CHAP no servidor de host do Windows, vá para [Considerações adicionais](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="9177c-164">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="9177c-165">Autenticação bidirecional ou mútua</span><span class="sxs-lookup"><span data-stu-id="9177c-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="9177c-166">Na autenticação bidirecional, o destino autentica o iniciador e, em seguida, o iniciador autentica o destino.</span><span class="sxs-lookup"><span data-stu-id="9177c-166">In bidirectional authentication, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="9177c-167">Esse procedimento exige que o usuário defina as configurações do iniciador CHAP, as configurações de CHAP inversas no dispositivo e no software Iniciador iSCSI no host.</span><span class="sxs-lookup"><span data-stu-id="9177c-167">This procedure requires the user to configure the CHAP initiator settings, reverse CHAP settings on the device, and iSCSI Initiator software on the host.</span></span> <span data-ttu-id="9177c-168">Os procedimentos a seguir descrevem as etapas para configurar a autenticação mútua no dispositivo e no host do Windows.</span><span class="sxs-lookup"><span data-stu-id="9177c-168">The following procedures describe the steps to configure mutual authentication on the device and on the Windows host.</span></span>

#### <a name="to-configure-your-device-for-mutual-authentication"></a><span data-ttu-id="9177c-169">Para configurar seu dispositivo para autenticação mútua</span><span class="sxs-lookup"><span data-stu-id="9177c-169">To configure your device for mutual authentication</span></span>

1. <span data-ttu-id="9177c-170">No Portal do Azure, acesse seu serviço do Gerenciador de Dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9177c-170">In the Azure portal, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="9177c-171">Clique em **Dispositivos** e selecione e clique em um dispositivo para o qual você deseja configurar o CHAP.</span><span class="sxs-lookup"><span data-stu-id="9177c-171">Click **Devices** and select and click a device you wish to configure CHAP for.</span></span> <span data-ttu-id="9177c-172">Acesse **Configurações do dispositivo > Segurança**.</span><span class="sxs-lookup"><span data-stu-id="9177c-172">Go to **Device settings > Security**.</span></span> <span data-ttu-id="9177c-173">Na folha **Configurações de segurança**, clique em **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="9177c-173">In the **Security settings** blade, click **CHAP**.</span></span>
   
    ![Destino do CHAP](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="9177c-175">Role para baixo nessa página e, na seção **Destino do CHAP** :</span><span class="sxs-lookup"><span data-stu-id="9177c-175">Scroll down on this page, and in the **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="9177c-176">Forneça um **Nome de usuário de CHAP reverso** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9177c-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="9177c-177">Forneça uma **Senha de CHAP reversa** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9177c-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="9177c-178">Confirme a senha.</span><span class="sxs-lookup"><span data-stu-id="9177c-178">Confirm the password.</span></span>
3. <span data-ttu-id="9177c-179">Na seção **Iniciador CHAP** :</span><span class="sxs-lookup"><span data-stu-id="9177c-179">In the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="9177c-180">Forneça um **nome de usuário** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9177c-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="9177c-181">Forneça uma **senha** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9177c-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="9177c-182">Confirme a senha.</span><span class="sxs-lookup"><span data-stu-id="9177c-182">Confirm the password.</span></span>

       ![Iniciador CHAP](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="9177c-184">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9177c-184">Click **Save**.</span></span> <span data-ttu-id="9177c-185">Uma mensagem de confirmação é exibida.</span><span class="sxs-lookup"><span data-stu-id="9177c-185">A confirmation message is displayed.</span></span> <span data-ttu-id="9177c-186">Clique em **OK** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="9177c-186">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-bidirectional-authentication-on-the-windows-host-server"></a><span data-ttu-id="9177c-187">Para configurar a autenticação bidirecional no servidor de host do Windows</span><span class="sxs-lookup"><span data-stu-id="9177c-187">To configure bidirectional authentication on the Windows host server</span></span>

1. <span data-ttu-id="9177c-188">No servidor de host do Windows, inicie o Iniciador iSCSI.</span><span class="sxs-lookup"><span data-stu-id="9177c-188">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="9177c-189">Na janela **Propriedades do Iniciador iSCSI**, clique na guia **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="9177c-189">In the **iSCSI Initiator Properties** window, click the **Configuration** tab.</span></span>
3. <span data-ttu-id="9177c-190">Clique em **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="9177c-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="9177c-191">Na caixa de diálogo **Segredo do CHAP Mútuo do Iniciador iSCSI** :</span><span class="sxs-lookup"><span data-stu-id="9177c-191">In the **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="9177c-192">Digite a **Senha do CHAP Inverso** que você configurou no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9177c-192">Type the **Reverse CHAP Password** that you configured in the Azure portal.</span></span>
   2. <span data-ttu-id="9177c-193">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9177c-193">Click **OK**.</span></span>
      
       ![Segredo do CHAP Mútuo do Iniciador iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="9177c-195">Clique na guia **Destinos** .</span><span class="sxs-lookup"><span data-stu-id="9177c-195">Click the **Targets** tab.</span></span>
6. <span data-ttu-id="9177c-196">Clique no botão **Conectar** .</span><span class="sxs-lookup"><span data-stu-id="9177c-196">Click the **Connect** button.</span></span> 
7. <span data-ttu-id="9177c-197">Na caixa de diálogo **Conectar ao Destino**, clique em **Avançado**.</span><span class="sxs-lookup"><span data-stu-id="9177c-197">In the **Connect To Target** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="9177c-198">Na caixa de diálogo **Propriedades Avançadas** :</span><span class="sxs-lookup"><span data-stu-id="9177c-198">In the **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="9177c-199">Marque a caixa de seleção **Habilitar logon CHAP** .</span><span class="sxs-lookup"><span data-stu-id="9177c-199">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="9177c-200">No campo **Nome** , forneça o nome de usuário especificado para o Iniciador CHAP no Portal clássico.</span><span class="sxs-lookup"><span data-stu-id="9177c-200">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="9177c-201">No campo **Segredo de destino** , forneça a senha especificada para o Iniciador CHAP no Portal clássico.</span><span class="sxs-lookup"><span data-stu-id="9177c-201">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="9177c-202">Marque a caixa de seleção **Executar a autenticação mútua** .</span><span class="sxs-lookup"><span data-stu-id="9177c-202">Select the **Perform mutual authentication** check box.</span></span>
      
       ![Configurações avançadas de autenticação mútua](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="9177c-204">Clique em **OK** para concluir a configuração CHAP</span><span class="sxs-lookup"><span data-stu-id="9177c-204">Click **OK** to complete the CHAP configuration</span></span>

<span data-ttu-id="9177c-205">Para saber mais sobre como configurar o CHAP no servidor de host do Windows, vá para [Considerações adicionais](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="9177c-205">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="9177c-206">Considerações adicionais</span><span class="sxs-lookup"><span data-stu-id="9177c-206">Additional considerations</span></span>

<span data-ttu-id="9177c-207">O recurso **Conexão Rápida** não dá suporte a conexões com o CHAP habilitado.</span><span class="sxs-lookup"><span data-stu-id="9177c-207">The **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="9177c-208">Quando o CHAP estiver habilitado, use o botão **Conectar** disponível na guia **Destinos** para se conectar a um destino.</span><span class="sxs-lookup"><span data-stu-id="9177c-208">When CHAP is enabled, make sure that you use the **Connect** button that is available on the **Targets** tab to connect to a target.</span></span>

![Conectar-se ao destino](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="9177c-210">Na caixa de diálogo **Conectar-se ao Destino** apresentada, marque a caixa de seleção **Adicionar esta conexão à lista de Destinos Favoritos**.</span><span class="sxs-lookup"><span data-stu-id="9177c-210">In the **Connect to Target** dialog box that is presented, select the **Add this connection to the list of Favorite Targets** check box.</span></span> <span data-ttu-id="9177c-211">Essa seleção garante que, sempre que o computador for reiniciado, ocorrerá uma tentativa de restaurar a conexão com os destinos favoritos de iSCSI.</span><span class="sxs-lookup"><span data-stu-id="9177c-211">This selection ensures that every time the computer restarts, an attempt is made to restore the connection to the iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="9177c-212">Erros durante a configuração</span><span class="sxs-lookup"><span data-stu-id="9177c-212">Errors during configuration</span></span>

<span data-ttu-id="9177c-213">Se a sua configuração do CHAP estiver incorreta, provavelmente você verá uma mensagem de erro de **Falha na autenticação** .</span><span class="sxs-lookup"><span data-stu-id="9177c-213">If your CHAP configuration is incorrect, then you are likely to see an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="9177c-214">Verificação da configuração do CHAP</span><span class="sxs-lookup"><span data-stu-id="9177c-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="9177c-215">Você pode verificar se o CHAP está sendo usado executando as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="9177c-215">You can verify that CHAP is being used by completing the following steps.</span></span>

#### <a name="to-verify-your-chap-configuration"></a><span data-ttu-id="9177c-216">Para verificar a configuração do CHAP</span><span class="sxs-lookup"><span data-stu-id="9177c-216">To verify your CHAP configuration</span></span>
1. <span data-ttu-id="9177c-217">Clique em **Destinos Favoritos**.</span><span class="sxs-lookup"><span data-stu-id="9177c-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="9177c-218">Selecione o destino para o qual você habilitou a autenticação.</span><span class="sxs-lookup"><span data-stu-id="9177c-218">Select the target for which you enabled authentication.</span></span>
3. <span data-ttu-id="9177c-219">Clique em **Detalhes**.</span><span class="sxs-lookup"><span data-stu-id="9177c-219">Click **Details**.</span></span>
   
    ![Destinos favoritos das propriedades do Iniciador iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="9177c-221">Na caixa de diálogo **Detalhes do Destino Favorito**, observe a entrada no campo **Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="9177c-221">In the **Favorite Target Details** dialog box, note the entry in the **Authentication** field.</span></span> <span data-ttu-id="9177c-222">Se a configuração for bem-sucedida, ela deverá dizer **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="9177c-222">If the configuration was successful, it should say **CHAP**.</span></span>
   
    ![Detalhes do destino favorito](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="9177c-224">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9177c-224">Next steps</span></span>

* <span data-ttu-id="9177c-225">Saiba mais sobre a [segurança do StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="9177c-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="9177c-226">Saiba mais sobre como [usar o serviço Gerenciador de Dispositivos do StorSimple para administrar o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="9177c-226">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

