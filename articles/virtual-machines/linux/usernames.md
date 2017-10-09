---
title: "aaaSelecting nomes de usuário para Linux | Microsoft Docs"
description: "Saiba como nomes de usuário tooselect para uma máquina virtual do Linux no Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="ebade-103">Selecionando nomes de usuário para Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="ebade-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="ebade-104">Quando você provisionar uma máquina virtual do Linux no Azure, você deve especificar nome de saudação de um usuário não raiz que você pode usar mais tarde toolog em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="ebade-104">When you provision a Linux virtual machine on Azure you must specify hello name of a non-root user that you can later use toolog into hello VM.</span></span> <span data-ttu-id="ebade-105">Você pode escolher nome de saudação do novo usuário do hello, ou se provisionamento via Olá portal clássico do Azure você pode aceitar o padrão de saudação nome "azureuser".</span><span class="sxs-lookup"><span data-stu-id="ebade-105">You may choose hello name of hello new user, or if provisioning via hello Azure classic portal you can accept hello default name "azureuser".</span></span>

<span data-ttu-id="ebade-106">Na maioria dos casos, esse usuário não existe na imagem base hello e será criado durante o processo de provisionamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="ebade-106">In most cases this user won't exist on hello base image and will be created during hello provisioning process.</span></span> <span data-ttu-id="ebade-107">Se o usuário Olá existir na imagem de VM base hello, agente do Linux Azure Olá simplesmente configura senha hello e/ou uma chave SSH para que o usuário com base nas informações de saudação que você especificou ao criar hello VM.</span><span class="sxs-lookup"><span data-stu-id="ebade-107">If hello user exists on hello base VM image, then hello Azure Linux agent simply configures hello password and/or SSH key for that user based on hello information you specified when creating hello VM.</span></span>

<span data-ttu-id="ebade-108">**Entretanto**, o Linux define um conjunto de nomes de usuário que não deve ser usado ao criar novos usuários.</span><span class="sxs-lookup"><span data-stu-id="ebade-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="ebade-109">Olá provisionamento processo será **falha** se você tentar tooprovision uma VM do Linux usando um usuário existente do sistema, que é definido como um usuário com UID 0-99.</span><span class="sxs-lookup"><span data-stu-id="ebade-109">hello provisioning process will **fail** if you try tooprovision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="ebade-110">Um exemplo típico é hello `root` usuário, que tem o UID 0.</span><span class="sxs-lookup"><span data-stu-id="ebade-110">A typical example is hello `root` user, which has UID 0.</span></span>

* <span data-ttu-id="ebade-111">Consulte também: [Base padrão do Linux - Intervalos de ID de usuário](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="ebade-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="ebade-112">a seguir Olá é uma lista de usuários comuns do sistema internas para CentOS e Ubuntu que você deve evitar usar ao provisionar uma máquina virtual do Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="ebade-112">hello following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="ebade-113">Essa lista é apenas um exemplo, consulte toohello documentação para sua distribuição tooensure esse nome de usuário Olá que você escolher não está em conflito com um usuário de sistema existente.</span><span class="sxs-lookup"><span data-stu-id="ebade-113">This list is just an example, please refer toohello documentation for your distribution tooensure that hello username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="ebade-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="ebade-114">CentOS</span></span>
* <span data-ttu-id="ebade-115">abrt</span><span class="sxs-lookup"><span data-stu-id="ebade-115">abrt</span></span>
* <span data-ttu-id="ebade-116">adm</span><span class="sxs-lookup"><span data-stu-id="ebade-116">adm</span></span>
* <span data-ttu-id="ebade-117">audio</span><span class="sxs-lookup"><span data-stu-id="ebade-117">audio</span></span>
* <span data-ttu-id="ebade-118">bin</span><span class="sxs-lookup"><span data-stu-id="ebade-118">bin</span></span>
* <span data-ttu-id="ebade-119">cdrom</span><span class="sxs-lookup"><span data-stu-id="ebade-119">cdrom</span></span>
* <span data-ttu-id="ebade-120">cgred</span><span class="sxs-lookup"><span data-stu-id="ebade-120">cgred</span></span>
* <span data-ttu-id="ebade-121">daemon</span><span class="sxs-lookup"><span data-stu-id="ebade-121">daemon</span></span>
* <span data-ttu-id="ebade-122">dbus</span><span class="sxs-lookup"><span data-stu-id="ebade-122">dbus</span></span>
* <span data-ttu-id="ebade-123">dialout</span><span class="sxs-lookup"><span data-stu-id="ebade-123">dialout</span></span>
* <span data-ttu-id="ebade-124">dip</span><span class="sxs-lookup"><span data-stu-id="ebade-124">dip</span></span>
* <span data-ttu-id="ebade-125">disk</span><span class="sxs-lookup"><span data-stu-id="ebade-125">disk</span></span>
* <span data-ttu-id="ebade-126">floppy</span><span class="sxs-lookup"><span data-stu-id="ebade-126">floppy</span></span>
* <span data-ttu-id="ebade-127">ftp</span><span class="sxs-lookup"><span data-stu-id="ebade-127">ftp</span></span>
* <span data-ttu-id="ebade-128">ftp</span><span class="sxs-lookup"><span data-stu-id="ebade-128">ftp</span></span>
* <span data-ttu-id="ebade-129">games</span><span class="sxs-lookup"><span data-stu-id="ebade-129">games</span></span>
* <span data-ttu-id="ebade-130">gopher</span><span class="sxs-lookup"><span data-stu-id="ebade-130">gopher</span></span>
* <span data-ttu-id="ebade-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="ebade-131">haldaemon</span></span>
* <span data-ttu-id="ebade-132">halt</span><span class="sxs-lookup"><span data-stu-id="ebade-132">halt</span></span>
* <span data-ttu-id="ebade-133">kmem</span><span class="sxs-lookup"><span data-stu-id="ebade-133">kmem</span></span>
* <span data-ttu-id="ebade-134">lock</span><span class="sxs-lookup"><span data-stu-id="ebade-134">lock</span></span>
* <span data-ttu-id="ebade-135">lp</span><span class="sxs-lookup"><span data-stu-id="ebade-135">lp</span></span>
* <span data-ttu-id="ebade-136">mail</span><span class="sxs-lookup"><span data-stu-id="ebade-136">mail</span></span>
* <span data-ttu-id="ebade-137">man</span><span class="sxs-lookup"><span data-stu-id="ebade-137">man</span></span>
* <span data-ttu-id="ebade-138">mem</span><span class="sxs-lookup"><span data-stu-id="ebade-138">mem</span></span>
* <span data-ttu-id="ebade-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="ebade-139">nfsnobody</span></span>
* <span data-ttu-id="ebade-140">nobody</span><span class="sxs-lookup"><span data-stu-id="ebade-140">nobody</span></span>
* <span data-ttu-id="ebade-141">ntp</span><span class="sxs-lookup"><span data-stu-id="ebade-141">ntp</span></span>
* <span data-ttu-id="ebade-142">operator</span><span class="sxs-lookup"><span data-stu-id="ebade-142">operator</span></span>
* <span data-ttu-id="ebade-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="ebade-143">oprofile</span></span>
* <span data-ttu-id="ebade-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="ebade-144">postdrop</span></span>
* <span data-ttu-id="ebade-145">postfix</span><span class="sxs-lookup"><span data-stu-id="ebade-145">postfix</span></span>
* <span data-ttu-id="ebade-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="ebade-146">qpidd</span></span>
* <span data-ttu-id="ebade-147">root</span><span class="sxs-lookup"><span data-stu-id="ebade-147">root</span></span>
* <span data-ttu-id="ebade-148">rpc</span><span class="sxs-lookup"><span data-stu-id="ebade-148">rpc</span></span>
* <span data-ttu-id="ebade-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="ebade-149">rpcuser</span></span>
* <span data-ttu-id="ebade-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="ebade-150">saslauth</span></span>
* <span data-ttu-id="ebade-151">shutdown</span><span class="sxs-lookup"><span data-stu-id="ebade-151">shutdown</span></span>
* <span data-ttu-id="ebade-152">slocate</span><span class="sxs-lookup"><span data-stu-id="ebade-152">slocate</span></span>
* <span data-ttu-id="ebade-153">sshd</span><span class="sxs-lookup"><span data-stu-id="ebade-153">sshd</span></span>
* <span data-ttu-id="ebade-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="ebade-154">stapdev</span></span>
* <span data-ttu-id="ebade-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="ebade-155">stapusr</span></span>
* <span data-ttu-id="ebade-156">sync</span><span class="sxs-lookup"><span data-stu-id="ebade-156">sync</span></span>
* <span data-ttu-id="ebade-157">sys</span><span class="sxs-lookup"><span data-stu-id="ebade-157">sys</span></span>
* <span data-ttu-id="ebade-158">tape</span><span class="sxs-lookup"><span data-stu-id="ebade-158">tape</span></span>
* <span data-ttu-id="ebade-159">test</span><span class="sxs-lookup"><span data-stu-id="ebade-159">test</span></span>
* <span data-ttu-id="ebade-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="ebade-160">tcpdump</span></span>
* <span data-ttu-id="ebade-161">tty</span><span class="sxs-lookup"><span data-stu-id="ebade-161">tty</span></span>
* <span data-ttu-id="ebade-162">users</span><span class="sxs-lookup"><span data-stu-id="ebade-162">users</span></span>
* <span data-ttu-id="ebade-163">utempter</span><span class="sxs-lookup"><span data-stu-id="ebade-163">utempter</span></span>
* <span data-ttu-id="ebade-164">utmp</span><span class="sxs-lookup"><span data-stu-id="ebade-164">utmp</span></span>
* <span data-ttu-id="ebade-165">uucp</span><span class="sxs-lookup"><span data-stu-id="ebade-165">uucp</span></span>
* <span data-ttu-id="ebade-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="ebade-166">vcsa</span></span>
* <span data-ttu-id="ebade-167">video</span><span class="sxs-lookup"><span data-stu-id="ebade-167">video</span></span>
* <span data-ttu-id="ebade-168">wheel</span><span class="sxs-lookup"><span data-stu-id="ebade-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="ebade-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ebade-169">Ubuntu</span></span>
* <span data-ttu-id="ebade-170">adm</span><span class="sxs-lookup"><span data-stu-id="ebade-170">adm</span></span>
* <span data-ttu-id="ebade-171">admin</span><span class="sxs-lookup"><span data-stu-id="ebade-171">admin</span></span>
* <span data-ttu-id="ebade-172">audio</span><span class="sxs-lookup"><span data-stu-id="ebade-172">audio</span></span>
* <span data-ttu-id="ebade-173">backup</span><span class="sxs-lookup"><span data-stu-id="ebade-173">backup</span></span>
* <span data-ttu-id="ebade-174">bin</span><span class="sxs-lookup"><span data-stu-id="ebade-174">bin</span></span>
* <span data-ttu-id="ebade-175">cdrom</span><span class="sxs-lookup"><span data-stu-id="ebade-175">cdrom</span></span>
* <span data-ttu-id="ebade-176">crontab</span><span class="sxs-lookup"><span data-stu-id="ebade-176">crontab</span></span>
* <span data-ttu-id="ebade-177">daemon</span><span class="sxs-lookup"><span data-stu-id="ebade-177">daemon</span></span>
* <span data-ttu-id="ebade-178">dialout</span><span class="sxs-lookup"><span data-stu-id="ebade-178">dialout</span></span>
* <span data-ttu-id="ebade-179">dip</span><span class="sxs-lookup"><span data-stu-id="ebade-179">dip</span></span>
* <span data-ttu-id="ebade-180">disk</span><span class="sxs-lookup"><span data-stu-id="ebade-180">disk</span></span>
* <span data-ttu-id="ebade-181">fax</span><span class="sxs-lookup"><span data-stu-id="ebade-181">fax</span></span>
* <span data-ttu-id="ebade-182">floppy</span><span class="sxs-lookup"><span data-stu-id="ebade-182">floppy</span></span>
* <span data-ttu-id="ebade-183">fuse</span><span class="sxs-lookup"><span data-stu-id="ebade-183">fuse</span></span>
* <span data-ttu-id="ebade-184">games</span><span class="sxs-lookup"><span data-stu-id="ebade-184">games</span></span>
* <span data-ttu-id="ebade-185">gnats</span><span class="sxs-lookup"><span data-stu-id="ebade-185">gnats</span></span>
* <span data-ttu-id="ebade-186">irc</span><span class="sxs-lookup"><span data-stu-id="ebade-186">irc</span></span>
* <span data-ttu-id="ebade-187">kmem</span><span class="sxs-lookup"><span data-stu-id="ebade-187">kmem</span></span>
* <span data-ttu-id="ebade-188">landscape</span><span class="sxs-lookup"><span data-stu-id="ebade-188">landscape</span></span>
* <span data-ttu-id="ebade-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="ebade-189">libuuid</span></span>
* <span data-ttu-id="ebade-190">list</span><span class="sxs-lookup"><span data-stu-id="ebade-190">list</span></span>
* <span data-ttu-id="ebade-191">lp</span><span class="sxs-lookup"><span data-stu-id="ebade-191">lp</span></span>
* <span data-ttu-id="ebade-192">mail</span><span class="sxs-lookup"><span data-stu-id="ebade-192">mail</span></span>
* <span data-ttu-id="ebade-193">man</span><span class="sxs-lookup"><span data-stu-id="ebade-193">man</span></span>
* <span data-ttu-id="ebade-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="ebade-194">messagebus</span></span>
* <span data-ttu-id="ebade-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="ebade-195">mlocate</span></span>
* <span data-ttu-id="ebade-196">netdev</span><span class="sxs-lookup"><span data-stu-id="ebade-196">netdev</span></span>
* <span data-ttu-id="ebade-197">news</span><span class="sxs-lookup"><span data-stu-id="ebade-197">news</span></span>
* <span data-ttu-id="ebade-198">nobody</span><span class="sxs-lookup"><span data-stu-id="ebade-198">nobody</span></span>
* <span data-ttu-id="ebade-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="ebade-199">nogroup</span></span>
* <span data-ttu-id="ebade-200">operator</span><span class="sxs-lookup"><span data-stu-id="ebade-200">operator</span></span>
* <span data-ttu-id="ebade-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="ebade-201">plugdev</span></span>
* <span data-ttu-id="ebade-202">proxy</span><span class="sxs-lookup"><span data-stu-id="ebade-202">proxy</span></span>
* <span data-ttu-id="ebade-203">root</span><span class="sxs-lookup"><span data-stu-id="ebade-203">root</span></span>
* <span data-ttu-id="ebade-204">sasl</span><span class="sxs-lookup"><span data-stu-id="ebade-204">sasl</span></span>
* <span data-ttu-id="ebade-205">shadow</span><span class="sxs-lookup"><span data-stu-id="ebade-205">shadow</span></span>
* <span data-ttu-id="ebade-206">src</span><span class="sxs-lookup"><span data-stu-id="ebade-206">src</span></span>
* <span data-ttu-id="ebade-207">ssh</span><span class="sxs-lookup"><span data-stu-id="ebade-207">ssh</span></span>
* <span data-ttu-id="ebade-208">sshd</span><span class="sxs-lookup"><span data-stu-id="ebade-208">sshd</span></span>
* <span data-ttu-id="ebade-209">staff</span><span class="sxs-lookup"><span data-stu-id="ebade-209">staff</span></span>
* <span data-ttu-id="ebade-210">sudo</span><span class="sxs-lookup"><span data-stu-id="ebade-210">sudo</span></span>
* <span data-ttu-id="ebade-211">sync</span><span class="sxs-lookup"><span data-stu-id="ebade-211">sync</span></span>
* <span data-ttu-id="ebade-212">sys</span><span class="sxs-lookup"><span data-stu-id="ebade-212">sys</span></span>
* <span data-ttu-id="ebade-213">syslog</span><span class="sxs-lookup"><span data-stu-id="ebade-213">syslog</span></span>
* <span data-ttu-id="ebade-214">tape</span><span class="sxs-lookup"><span data-stu-id="ebade-214">tape</span></span>
* <span data-ttu-id="ebade-215">tty</span><span class="sxs-lookup"><span data-stu-id="ebade-215">tty</span></span>
* <span data-ttu-id="ebade-216">users</span><span class="sxs-lookup"><span data-stu-id="ebade-216">users</span></span>
* <span data-ttu-id="ebade-217">utmp</span><span class="sxs-lookup"><span data-stu-id="ebade-217">utmp</span></span>
* <span data-ttu-id="ebade-218">uucp</span><span class="sxs-lookup"><span data-stu-id="ebade-218">uucp</span></span>
* <span data-ttu-id="ebade-219">video</span><span class="sxs-lookup"><span data-stu-id="ebade-219">video</span></span>
* <span data-ttu-id="ebade-220">voice</span><span class="sxs-lookup"><span data-stu-id="ebade-220">voice</span></span>
* <span data-ttu-id="ebade-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="ebade-221">whoopsie</span></span>
* <span data-ttu-id="ebade-222">www-data</span><span class="sxs-lookup"><span data-stu-id="ebade-222">www-data</span></span>

