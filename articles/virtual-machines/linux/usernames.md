---
title: "Selecionando nomes de usuário para Linux | Microsoft Docs"
description: "Saiba como selecionar nomes de usuário para uma máquina virtual Linux no Azure."
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
ms.openlocfilehash: 1874d72e5f88816036667932371ff28704d186c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="5a057-103">Selecionando nomes de usuário para Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="5a057-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="5a057-104">Ao provisionar uma máquina virtual do Linux no Azure, você deve especificar o nome de um usuário não raiz que possa usar posteriormente para fazer logon na VM.</span><span class="sxs-lookup"><span data-stu-id="5a057-104">When you provision a Linux virtual machine on Azure you must specify the name of a non-root user that you can later use to log into the VM.</span></span> <span data-ttu-id="5a057-105">Você pode escolher o nome do novo usuário, ou se o provisionamento for por meio do portal clássico do Azure, você pode aceitar o nome padrão "azureuser".</span><span class="sxs-lookup"><span data-stu-id="5a057-105">You may choose the name of the new user, or if provisioning via the Azure classic portal you can accept the default name "azureuser".</span></span>

<span data-ttu-id="5a057-106">Na maioria dos casos, esse usuário não existe na imagem de base e é criado durante o processo de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="5a057-106">In most cases this user won't exist on the base image and will be created during the provisioning process.</span></span> <span data-ttu-id="5a057-107">Se o usuário já existir na imagem de base da máquina virtual, o agente do Linux do Azure simplesmente configurará a senha e/ou chave SSH para o usuário com base nas informações especificadas ao criar a VM.</span><span class="sxs-lookup"><span data-stu-id="5a057-107">If the user exists on the base VM image, then the Azure Linux agent simply configures the password and/or SSH key for that user based on the information you specified when creating the VM.</span></span>

<span data-ttu-id="5a057-108">**Entretanto**, o Linux define um conjunto de nomes de usuário que não deve ser usado ao criar novos usuários.</span><span class="sxs-lookup"><span data-stu-id="5a057-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="5a057-109">O processo de provisionamento irá **falhar** se você tentar provisionar uma máquina virtual Linux usando um usuário existente que esteja definido como um usuário com UID 0-99.</span><span class="sxs-lookup"><span data-stu-id="5a057-109">The provisioning process will **fail** if you try to provision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="5a057-110">Um exemplo típico é o usuário `root` , que tem o UID 0.</span><span class="sxs-lookup"><span data-stu-id="5a057-110">A typical example is the `root` user, which has UID 0.</span></span>

* <span data-ttu-id="5a057-111">Consulte também: [Base padrão do Linux - Intervalos de ID de usuário](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="5a057-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="5a057-112">A seguir está uma lista de usuários do sistema internos e comuns para o CentOS e Ubuntu que você deve evitar usar ao provisionar uma máquina virtual do Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="5a057-112">The following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="5a057-113">Essa lista é apenas um exemplo. Consulte a documentação de sua distribuição para garantir que o nome de usuário escolhido não entra em conflito com um usuário do sistema existente.</span><span class="sxs-lookup"><span data-stu-id="5a057-113">This list is just an example, please refer to the documentation for your distribution to ensure that the username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="5a057-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="5a057-114">CentOS</span></span>
* <span data-ttu-id="5a057-115">abrt</span><span class="sxs-lookup"><span data-stu-id="5a057-115">abrt</span></span>
* <span data-ttu-id="5a057-116">adm</span><span class="sxs-lookup"><span data-stu-id="5a057-116">adm</span></span>
* <span data-ttu-id="5a057-117">audio</span><span class="sxs-lookup"><span data-stu-id="5a057-117">audio</span></span>
* <span data-ttu-id="5a057-118">bin</span><span class="sxs-lookup"><span data-stu-id="5a057-118">bin</span></span>
* <span data-ttu-id="5a057-119">cdrom</span><span class="sxs-lookup"><span data-stu-id="5a057-119">cdrom</span></span>
* <span data-ttu-id="5a057-120">cgred</span><span class="sxs-lookup"><span data-stu-id="5a057-120">cgred</span></span>
* <span data-ttu-id="5a057-121">daemon</span><span class="sxs-lookup"><span data-stu-id="5a057-121">daemon</span></span>
* <span data-ttu-id="5a057-122">dbus</span><span class="sxs-lookup"><span data-stu-id="5a057-122">dbus</span></span>
* <span data-ttu-id="5a057-123">dialout</span><span class="sxs-lookup"><span data-stu-id="5a057-123">dialout</span></span>
* <span data-ttu-id="5a057-124">dip</span><span class="sxs-lookup"><span data-stu-id="5a057-124">dip</span></span>
* <span data-ttu-id="5a057-125">disk</span><span class="sxs-lookup"><span data-stu-id="5a057-125">disk</span></span>
* <span data-ttu-id="5a057-126">floppy</span><span class="sxs-lookup"><span data-stu-id="5a057-126">floppy</span></span>
* <span data-ttu-id="5a057-127">ftp</span><span class="sxs-lookup"><span data-stu-id="5a057-127">ftp</span></span>
* <span data-ttu-id="5a057-128">ftp</span><span class="sxs-lookup"><span data-stu-id="5a057-128">ftp</span></span>
* <span data-ttu-id="5a057-129">games</span><span class="sxs-lookup"><span data-stu-id="5a057-129">games</span></span>
* <span data-ttu-id="5a057-130">gopher</span><span class="sxs-lookup"><span data-stu-id="5a057-130">gopher</span></span>
* <span data-ttu-id="5a057-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="5a057-131">haldaemon</span></span>
* <span data-ttu-id="5a057-132">halt</span><span class="sxs-lookup"><span data-stu-id="5a057-132">halt</span></span>
* <span data-ttu-id="5a057-133">kmem</span><span class="sxs-lookup"><span data-stu-id="5a057-133">kmem</span></span>
* <span data-ttu-id="5a057-134">lock</span><span class="sxs-lookup"><span data-stu-id="5a057-134">lock</span></span>
* <span data-ttu-id="5a057-135">lp</span><span class="sxs-lookup"><span data-stu-id="5a057-135">lp</span></span>
* <span data-ttu-id="5a057-136">mail</span><span class="sxs-lookup"><span data-stu-id="5a057-136">mail</span></span>
* <span data-ttu-id="5a057-137">man</span><span class="sxs-lookup"><span data-stu-id="5a057-137">man</span></span>
* <span data-ttu-id="5a057-138">mem</span><span class="sxs-lookup"><span data-stu-id="5a057-138">mem</span></span>
* <span data-ttu-id="5a057-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="5a057-139">nfsnobody</span></span>
* <span data-ttu-id="5a057-140">nobody</span><span class="sxs-lookup"><span data-stu-id="5a057-140">nobody</span></span>
* <span data-ttu-id="5a057-141">ntp</span><span class="sxs-lookup"><span data-stu-id="5a057-141">ntp</span></span>
* <span data-ttu-id="5a057-142">operator</span><span class="sxs-lookup"><span data-stu-id="5a057-142">operator</span></span>
* <span data-ttu-id="5a057-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="5a057-143">oprofile</span></span>
* <span data-ttu-id="5a057-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="5a057-144">postdrop</span></span>
* <span data-ttu-id="5a057-145">postfix</span><span class="sxs-lookup"><span data-stu-id="5a057-145">postfix</span></span>
* <span data-ttu-id="5a057-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="5a057-146">qpidd</span></span>
* <span data-ttu-id="5a057-147">root</span><span class="sxs-lookup"><span data-stu-id="5a057-147">root</span></span>
* <span data-ttu-id="5a057-148">rpc</span><span class="sxs-lookup"><span data-stu-id="5a057-148">rpc</span></span>
* <span data-ttu-id="5a057-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="5a057-149">rpcuser</span></span>
* <span data-ttu-id="5a057-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="5a057-150">saslauth</span></span>
* <span data-ttu-id="5a057-151">shutdown</span><span class="sxs-lookup"><span data-stu-id="5a057-151">shutdown</span></span>
* <span data-ttu-id="5a057-152">slocate</span><span class="sxs-lookup"><span data-stu-id="5a057-152">slocate</span></span>
* <span data-ttu-id="5a057-153">sshd</span><span class="sxs-lookup"><span data-stu-id="5a057-153">sshd</span></span>
* <span data-ttu-id="5a057-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="5a057-154">stapdev</span></span>
* <span data-ttu-id="5a057-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="5a057-155">stapusr</span></span>
* <span data-ttu-id="5a057-156">sync</span><span class="sxs-lookup"><span data-stu-id="5a057-156">sync</span></span>
* <span data-ttu-id="5a057-157">sys</span><span class="sxs-lookup"><span data-stu-id="5a057-157">sys</span></span>
* <span data-ttu-id="5a057-158">tape</span><span class="sxs-lookup"><span data-stu-id="5a057-158">tape</span></span>
* <span data-ttu-id="5a057-159">test</span><span class="sxs-lookup"><span data-stu-id="5a057-159">test</span></span>
* <span data-ttu-id="5a057-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="5a057-160">tcpdump</span></span>
* <span data-ttu-id="5a057-161">tty</span><span class="sxs-lookup"><span data-stu-id="5a057-161">tty</span></span>
* <span data-ttu-id="5a057-162">users</span><span class="sxs-lookup"><span data-stu-id="5a057-162">users</span></span>
* <span data-ttu-id="5a057-163">utempter</span><span class="sxs-lookup"><span data-stu-id="5a057-163">utempter</span></span>
* <span data-ttu-id="5a057-164">utmp</span><span class="sxs-lookup"><span data-stu-id="5a057-164">utmp</span></span>
* <span data-ttu-id="5a057-165">uucp</span><span class="sxs-lookup"><span data-stu-id="5a057-165">uucp</span></span>
* <span data-ttu-id="5a057-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="5a057-166">vcsa</span></span>
* <span data-ttu-id="5a057-167">video</span><span class="sxs-lookup"><span data-stu-id="5a057-167">video</span></span>
* <span data-ttu-id="5a057-168">wheel</span><span class="sxs-lookup"><span data-stu-id="5a057-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="5a057-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="5a057-169">Ubuntu</span></span>
* <span data-ttu-id="5a057-170">adm</span><span class="sxs-lookup"><span data-stu-id="5a057-170">adm</span></span>
* <span data-ttu-id="5a057-171">admin</span><span class="sxs-lookup"><span data-stu-id="5a057-171">admin</span></span>
* <span data-ttu-id="5a057-172">audio</span><span class="sxs-lookup"><span data-stu-id="5a057-172">audio</span></span>
* <span data-ttu-id="5a057-173">backup</span><span class="sxs-lookup"><span data-stu-id="5a057-173">backup</span></span>
* <span data-ttu-id="5a057-174">bin</span><span class="sxs-lookup"><span data-stu-id="5a057-174">bin</span></span>
* <span data-ttu-id="5a057-175">cdrom</span><span class="sxs-lookup"><span data-stu-id="5a057-175">cdrom</span></span>
* <span data-ttu-id="5a057-176">crontab</span><span class="sxs-lookup"><span data-stu-id="5a057-176">crontab</span></span>
* <span data-ttu-id="5a057-177">daemon</span><span class="sxs-lookup"><span data-stu-id="5a057-177">daemon</span></span>
* <span data-ttu-id="5a057-178">dialout</span><span class="sxs-lookup"><span data-stu-id="5a057-178">dialout</span></span>
* <span data-ttu-id="5a057-179">dip</span><span class="sxs-lookup"><span data-stu-id="5a057-179">dip</span></span>
* <span data-ttu-id="5a057-180">disk</span><span class="sxs-lookup"><span data-stu-id="5a057-180">disk</span></span>
* <span data-ttu-id="5a057-181">fax</span><span class="sxs-lookup"><span data-stu-id="5a057-181">fax</span></span>
* <span data-ttu-id="5a057-182">floppy</span><span class="sxs-lookup"><span data-stu-id="5a057-182">floppy</span></span>
* <span data-ttu-id="5a057-183">fuse</span><span class="sxs-lookup"><span data-stu-id="5a057-183">fuse</span></span>
* <span data-ttu-id="5a057-184">games</span><span class="sxs-lookup"><span data-stu-id="5a057-184">games</span></span>
* <span data-ttu-id="5a057-185">gnats</span><span class="sxs-lookup"><span data-stu-id="5a057-185">gnats</span></span>
* <span data-ttu-id="5a057-186">irc</span><span class="sxs-lookup"><span data-stu-id="5a057-186">irc</span></span>
* <span data-ttu-id="5a057-187">kmem</span><span class="sxs-lookup"><span data-stu-id="5a057-187">kmem</span></span>
* <span data-ttu-id="5a057-188">landscape</span><span class="sxs-lookup"><span data-stu-id="5a057-188">landscape</span></span>
* <span data-ttu-id="5a057-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="5a057-189">libuuid</span></span>
* <span data-ttu-id="5a057-190">list</span><span class="sxs-lookup"><span data-stu-id="5a057-190">list</span></span>
* <span data-ttu-id="5a057-191">lp</span><span class="sxs-lookup"><span data-stu-id="5a057-191">lp</span></span>
* <span data-ttu-id="5a057-192">mail</span><span class="sxs-lookup"><span data-stu-id="5a057-192">mail</span></span>
* <span data-ttu-id="5a057-193">man</span><span class="sxs-lookup"><span data-stu-id="5a057-193">man</span></span>
* <span data-ttu-id="5a057-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="5a057-194">messagebus</span></span>
* <span data-ttu-id="5a057-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="5a057-195">mlocate</span></span>
* <span data-ttu-id="5a057-196">netdev</span><span class="sxs-lookup"><span data-stu-id="5a057-196">netdev</span></span>
* <span data-ttu-id="5a057-197">news</span><span class="sxs-lookup"><span data-stu-id="5a057-197">news</span></span>
* <span data-ttu-id="5a057-198">nobody</span><span class="sxs-lookup"><span data-stu-id="5a057-198">nobody</span></span>
* <span data-ttu-id="5a057-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="5a057-199">nogroup</span></span>
* <span data-ttu-id="5a057-200">operator</span><span class="sxs-lookup"><span data-stu-id="5a057-200">operator</span></span>
* <span data-ttu-id="5a057-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="5a057-201">plugdev</span></span>
* <span data-ttu-id="5a057-202">proxy</span><span class="sxs-lookup"><span data-stu-id="5a057-202">proxy</span></span>
* <span data-ttu-id="5a057-203">root</span><span class="sxs-lookup"><span data-stu-id="5a057-203">root</span></span>
* <span data-ttu-id="5a057-204">sasl</span><span class="sxs-lookup"><span data-stu-id="5a057-204">sasl</span></span>
* <span data-ttu-id="5a057-205">shadow</span><span class="sxs-lookup"><span data-stu-id="5a057-205">shadow</span></span>
* <span data-ttu-id="5a057-206">src</span><span class="sxs-lookup"><span data-stu-id="5a057-206">src</span></span>
* <span data-ttu-id="5a057-207">ssh</span><span class="sxs-lookup"><span data-stu-id="5a057-207">ssh</span></span>
* <span data-ttu-id="5a057-208">sshd</span><span class="sxs-lookup"><span data-stu-id="5a057-208">sshd</span></span>
* <span data-ttu-id="5a057-209">staff</span><span class="sxs-lookup"><span data-stu-id="5a057-209">staff</span></span>
* <span data-ttu-id="5a057-210">sudo</span><span class="sxs-lookup"><span data-stu-id="5a057-210">sudo</span></span>
* <span data-ttu-id="5a057-211">sync</span><span class="sxs-lookup"><span data-stu-id="5a057-211">sync</span></span>
* <span data-ttu-id="5a057-212">sys</span><span class="sxs-lookup"><span data-stu-id="5a057-212">sys</span></span>
* <span data-ttu-id="5a057-213">syslog</span><span class="sxs-lookup"><span data-stu-id="5a057-213">syslog</span></span>
* <span data-ttu-id="5a057-214">tape</span><span class="sxs-lookup"><span data-stu-id="5a057-214">tape</span></span>
* <span data-ttu-id="5a057-215">tty</span><span class="sxs-lookup"><span data-stu-id="5a057-215">tty</span></span>
* <span data-ttu-id="5a057-216">users</span><span class="sxs-lookup"><span data-stu-id="5a057-216">users</span></span>
* <span data-ttu-id="5a057-217">utmp</span><span class="sxs-lookup"><span data-stu-id="5a057-217">utmp</span></span>
* <span data-ttu-id="5a057-218">uucp</span><span class="sxs-lookup"><span data-stu-id="5a057-218">uucp</span></span>
* <span data-ttu-id="5a057-219">video</span><span class="sxs-lookup"><span data-stu-id="5a057-219">video</span></span>
* <span data-ttu-id="5a057-220">voice</span><span class="sxs-lookup"><span data-stu-id="5a057-220">voice</span></span>
* <span data-ttu-id="5a057-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="5a057-221">whoopsie</span></span>
* <span data-ttu-id="5a057-222">www-data</span><span class="sxs-lookup"><span data-stu-id="5a057-222">www-data</span></span>

