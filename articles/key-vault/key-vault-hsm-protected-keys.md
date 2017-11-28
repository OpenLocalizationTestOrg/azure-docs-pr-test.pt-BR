---
title: aaaHow toogenerate e transferir chaves protegidas por HSM para o Cofre de chaves do Azure | Microsoft Docs
description: "Use toohelp neste artigo, planejar, gerar e transferir sua própria toouse chaves protegidas por HSM com o Cofre de chaves do Azure. Também conhecido como BYOK ou Traga sua própria chave."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="74cba-104">Como toogenerate e transferir chaves protegidas por HSM para o Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="74cba-104">How toogenerate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="74cba-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="74cba-105">Introduction</span></span>
<span data-ttu-id="74cba-106">Para garantia extra, quando você usar o Cofre de chaves do Azure, você pode importar ou gerar chaves em módulos de segurança de hardware (HSM) que nunca deixam o limite do HSM hello.</span><span class="sxs-lookup"><span data-stu-id="74cba-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="74cba-107">Este cenário é geralmente chamado tooas *Traga sua própria chave*, ou BYOK.</span><span class="sxs-lookup"><span data-stu-id="74cba-107">This scenario is often referred tooas *bring your own key*, or BYOK.</span></span> <span data-ttu-id="74cba-108">Olá HSMs são FIPS 140-2 nível 2 validado.</span><span class="sxs-lookup"><span data-stu-id="74cba-108">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="74cba-109">Cofre de chaves do Azure usa a família Thales nShield dos HSMs tooprotect suas chaves.</span><span class="sxs-lookup"><span data-stu-id="74cba-109">Azure Key Vault uses Thales nShield family of HSMs tooprotect your keys.</span></span>

<span data-ttu-id="74cba-110">Use as informações de saudação toohelp neste tópico, você planejar, gera e transferir toouse suas próprias chaves protegidas por HSM com o Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="74cba-110">Use hello information in this topic toohelp you plan for, generate, and then transfer your own HSM-protected keys toouse with Azure Key Vault.</span></span>

<span data-ttu-id="74cba-111">Essa funcionalidade não está disponível para o Azure China.</span><span class="sxs-lookup"><span data-stu-id="74cba-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="74cba-112">Para obter mais informações sobre o Cofre da Chave do Azure, consulte [O que é o Cofre da Chave do Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="74cba-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="74cba-113">Para obter um tutorial de Introdução, que inclui a criação de um Cofre da Chave para chaves de HSM protegido, consulte [Introdução ao Cofre da Chave do Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="74cba-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="74cba-114">Obter mais informações sobre como gerar e transferir uma chave protegida por HSM pela Olá Internet:</span><span class="sxs-lookup"><span data-stu-id="74cba-114">More information about generating and transferring an HSM-protected key over hello Internet:</span></span>

* <span data-ttu-id="74cba-115">Você gera a chave de saudação de uma estação de trabalho offline, o que reduz a superfície de ataque de saudação.</span><span class="sxs-lookup"><span data-stu-id="74cba-115">You generate hello key from an offline workstation, which reduces hello attack surface.</span></span>
* <span data-ttu-id="74cba-116">chave de saudação é criptografada com uma chave de troca de chave (KEK), que permanece criptografada até que ele é transferido toohello HSMs do Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="74cba-116">hello key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred toohello Azure Key Vault HSMs.</span></span> <span data-ttu-id="74cba-117">Apenas Olá versão criptografada da chave de deixa a estação de trabalho original Olá.</span><span class="sxs-lookup"><span data-stu-id="74cba-117">Only hello encrypted version of your key leaves hello original workstation.</span></span>
* <span data-ttu-id="74cba-118">saudação de conjunto de ferramentas define propriedades na chave de locatário que associa sua chave toohello mundo de segurança do Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="74cba-118">hello toolset sets properties on your tenant key that binds your key toohello Azure Key Vault security world.</span></span> <span data-ttu-id="74cba-119">Assim após Olá HSMs do Cofre de chave do Azure receberem e descriptografarem a chave, somente esses HSMs poderão usá-lo.</span><span class="sxs-lookup"><span data-stu-id="74cba-119">So after hello Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="74cba-120">A chave não pode ser exportada.</span><span class="sxs-lookup"><span data-stu-id="74cba-120">Your key cannot be exported.</span></span> <span data-ttu-id="74cba-121">Essa associação é imposta pelo Olá HSMs da Thales.</span><span class="sxs-lookup"><span data-stu-id="74cba-121">This binding is enforced by hello Thales HSMs.</span></span>
* <span data-ttu-id="74cba-122">Olá chave de troca de chave (KEK) que é usado tooencrypt sua chave é gerada dentro Olá HSMs do Cofre de chave do Azure e não é exportável.</span><span class="sxs-lookup"><span data-stu-id="74cba-122">hello Key Exchange Key (KEK) that is used tooencrypt your key is generated inside hello Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="74cba-123">Olá HSMs impõem que não pode haver nenhuma versão clara do hello KEK fora Olá HSMs.</span><span class="sxs-lookup"><span data-stu-id="74cba-123">hello HSMs enforce that there can be no clear version of hello KEK outside hello HSMs.</span></span> <span data-ttu-id="74cba-124">Além disso, a saudação de conjunto de ferramentas inclui Atestado da Thales que Olá KEK não é exportável e foi gerada dentro de um HSM original que foi fabricado pela Thales.</span><span class="sxs-lookup"><span data-stu-id="74cba-124">In addition, hello toolset includes attestation from Thales that hello KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="74cba-125">saudação de conjunto de ferramentas inclui Atestado da Thales de que Olá mundo de segurança também foi gerado em um HSM original fabricado pela Thales o Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="74cba-125">hello toolset includes attestation from Thales that hello Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="74cba-126">Este Atestado prova tooyou que a Microsoft está usando hardware original.</span><span class="sxs-lookup"><span data-stu-id="74cba-126">This attestation proves tooyou that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="74cba-127">A Microsoft usa KEKs separadas e separa os universos de segurança em cada região geográfica.</span><span class="sxs-lookup"><span data-stu-id="74cba-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="74cba-128">Essa separação garante que a chave pode ser usada apenas em data centers na região de saudação em que você criptografou.</span><span class="sxs-lookup"><span data-stu-id="74cba-128">This separation ensures that your key can be used only in data centers in hello region in which you encrypted it.</span></span> <span data-ttu-id="74cba-129">Por exemplo, uma chave de um cliente europeu não pode ser usada em data centers na América do Norte ou na Ásia.</span><span class="sxs-lookup"><span data-stu-id="74cba-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="74cba-130">Para obter mais informações sobre serviços HSMs da Thales e da Microsoft</span><span class="sxs-lookup"><span data-stu-id="74cba-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="74cba-131">A Thales e-Security é uma fornecedora líder global de criptografia de dados e cyber segurança soluções toohello serviços financeiros, alta tecnologia, manufatura, governo e setores de tecnologia.</span><span class="sxs-lookup"><span data-stu-id="74cba-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions toohello financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="74cba-132">Com um 40 anos acompanhar de proteção de informações corporativas e governamentais, as soluções Thales são usadas por quatro das cinco empresas maiores de energia e aeroespacial hello.</span><span class="sxs-lookup"><span data-stu-id="74cba-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of hello five largest energy and aerospace companies.</span></span> <span data-ttu-id="74cba-133">Suas soluções também são usadas por 22 países da OTAN e protegem mais de 80 porcento das transações de pagamento em todo o mundo.</span><span class="sxs-lookup"><span data-stu-id="74cba-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="74cba-134">A Microsoft tem colaborado com estado de saudação do Thales tooenhance de arte HSMs.</span><span class="sxs-lookup"><span data-stu-id="74cba-134">Microsoft has collaborated with Thales tooenhance hello state of art for HSMs.</span></span> <span data-ttu-id="74cba-135">Essas melhorias permitem benefícios típicos de saudação de tooget de serviços hospedados sem abrir mão do controle sobre as chaves.</span><span class="sxs-lookup"><span data-stu-id="74cba-135">These enhancements enable you tooget hello typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="74cba-136">Especificamente, essas melhorias permitem que a Microsoft gerenciar Olá HSMs para que você não precisa.</span><span class="sxs-lookup"><span data-stu-id="74cba-136">Specifically, these enhancements let Microsoft manage hello HSMs so that you do not have to.</span></span> <span data-ttu-id="74cba-137">Como uma nuvem de serviço, o Azure Key Vault é dimensionado a curto prazo toomeet picos de uso da sua organização.</span><span class="sxs-lookup"><span data-stu-id="74cba-137">As a cloud service, Azure Key Vault scales up at short notice toomeet your organization’s usage spikes.</span></span> <span data-ttu-id="74cba-138">AT Olá mesmo tempo, sua chave está protegida dentro dos HSMs da Microsoft: você mantém controle sobre o ciclo de vida Olá porque gerar chave hello e transferi-la HSMs do tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="74cba-138">At hello same time, your key is protected inside Microsoft’s HSMs: You retain control over hello key lifecycle because you generate hello key and transfer it tooMicrosoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="74cba-139">Implementando o Traga a sua própria chave (BYOK) para o Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="74cba-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="74cba-140">Olá use informações e os procedimentos a seguir se você gerar sua própria chave protegida por HSM e transferi-la tooAzure Cofre de chave — Olá traga seu próprio cenário da chave (BYOK).</span><span class="sxs-lookup"><span data-stu-id="74cba-140">Use hello following information and procedures if you will generate your own HSM-protected key and then transfer it tooAzure Key Vault—hello bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="74cba-141">Pré-requisitos para BYOK</span><span class="sxs-lookup"><span data-stu-id="74cba-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="74cba-142">Consulte o hello para obter uma lista de pré-requisitos para a tabela a seguir Traga sua própria chave (BYOK) para o Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="74cba-142">See hello following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="74cba-143">Requisito</span><span class="sxs-lookup"><span data-stu-id="74cba-143">Requirement</span></span> | <span data-ttu-id="74cba-144">Mais informações</span><span class="sxs-lookup"><span data-stu-id="74cba-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="74cba-145">Um tooAzure de assinatura</span><span class="sxs-lookup"><span data-stu-id="74cba-145">A subscription tooAzure</span></span> |<span data-ttu-id="74cba-146">toocreate um cofre de chaves do Azure, você precisa de uma assinatura do Azure: [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="74cba-146">toocreate an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="74cba-147">Olá chaves protegidas por HSM do Cofre de chave do Azure Premium serviço camada toosupport</span><span class="sxs-lookup"><span data-stu-id="74cba-147">hello Azure Key Vault Premium service tier toosupport HSM-protected keys</span></span> |<span data-ttu-id="74cba-148">Para obter mais informações sobre as camadas de serviço hello e recursos para o Cofre de chaves do Azure, consulte Olá [preços do Cofre de chaves do Azure](https://azure.microsoft.com/pricing/details/key-vault/) site.</span><span class="sxs-lookup"><span data-stu-id="74cba-148">For more information about hello service tiers and capabilities for Azure Key Vault, see hello [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="74cba-149">HSM da Thales, smartcards e software de suporte</span><span class="sxs-lookup"><span data-stu-id="74cba-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="74cba-150">Você deve ter acesso tooa Thales Hardware Security Module e conhecimento operacional básico dos HSMs da Thales.</span><span class="sxs-lookup"><span data-stu-id="74cba-150">You must have access tooa Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="74cba-151">Consulte [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) para lista de saudação de modelos compatíveis ou toopurchase um HSM, se você não tiver um.</span><span class="sxs-lookup"><span data-stu-id="74cba-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for hello list of compatible models, or toopurchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="74cba-152">Olá hardware e software a seguir:</span><span class="sxs-lookup"><span data-stu-id="74cba-152">hello following hardware and software:</span></span><ol><li><span data-ttu-id="74cba-153">Uma estação de trabalho x64 offline com, no mínimo, um sistema operacional Windows 7 e software Thales nShield, versão 11.50 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="74cba-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="74cba-154">Se essa estação de trabalho executa o Windows 7, você deve [instalar o Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span><span class="sxs-lookup"><span data-stu-id="74cba-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="74cba-155">Uma estação de trabalho que é toohello conectado à Internet e tem um sistema de operacional Windows mínimo do Windows 7 e [Azure PowerShell](/powershell/azure/overview) **versão mínima 1.1.0** instalado.</span><span class="sxs-lookup"><span data-stu-id="74cba-155">A workstation that is connected toohello Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="74cba-156">Uma unidade USB ou outro dispositivo de armazenamento portátil que tenha pelo menos 16 MB de espaço livre.</span><span class="sxs-lookup"><span data-stu-id="74cba-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="74cba-157">Por motivos de segurança, recomendamos que Olá primeira estação de trabalho não está conectado tooa rede.</span><span class="sxs-lookup"><span data-stu-id="74cba-157">For security reasons, we recommend that hello first workstation is not connected tooa network.</span></span> <span data-ttu-id="74cba-158">No entanto, essa recomendação não é programaticamente aplicada.</span><span class="sxs-lookup"><span data-stu-id="74cba-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="74cba-159">Observe que nas instruções de saudação que seguem, essa estação de trabalho é estação de trabalho chamado tooas Olá desconectado.</span><span class="sxs-lookup"><span data-stu-id="74cba-159">Note that in hello instructions that follow, this workstation is referred tooas hello disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="74cba-160">Além disso, se a chave de locatário for para uma rede de produção, recomendamos que você use uma estação de trabalho separada e segundo toodownload Olá conjunto de ferramentas e carregamento Olá chave de locatário.</span><span class="sxs-lookup"><span data-stu-id="74cba-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation toodownload hello toolset and upload hello tenant key.</span></span> <span data-ttu-id="74cba-161">Mas para fins de teste, você pode usar Olá mesma estação de trabalho como Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="74cba-161">But for testing purposes, you can use hello same workstation as hello first one.</span></span><br/><br/><span data-ttu-id="74cba-162">Observe que nas instruções de saudação que seguem, essa segunda estação de trabalho é chamado tooas Olá estação de trabalho conectada à Internet.</span><span class="sxs-lookup"><span data-stu-id="74cba-162">Note that in hello instructions that follow, this second workstation is referred tooas hello Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a><span data-ttu-id="74cba-163">Gerar e transferir sua chave tooAzure HSM do Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="74cba-163">Generate and transfer your key tooAzure Key Vault HSM</span></span>
<span data-ttu-id="74cba-164">Você usará Olá toogenerate de cinco etapas a seguir e transferir sua chave tooan HSM do Cofre de chaves do Azure:</span><span class="sxs-lookup"><span data-stu-id="74cba-164">You will use hello following five steps toogenerate and transfer your key tooan Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="74cba-165">Etapa 1: preparar sua estação de trabalho conectada à Internet</span><span class="sxs-lookup"><span data-stu-id="74cba-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="74cba-166">Etapa 2: preparar sua estação de trabalho desconectada</span><span class="sxs-lookup"><span data-stu-id="74cba-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="74cba-167">Etapa 3: Gerar a sua chave</span><span class="sxs-lookup"><span data-stu-id="74cba-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="74cba-168">Etapa 4: Preparar a sua chave para transferência</span><span class="sxs-lookup"><span data-stu-id="74cba-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="74cba-169">Etapa 5: Transferir sua chave tooAzure Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="74cba-169">Step 5: Transfer your key tooAzure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="74cba-170">Etapa 1: preparar sua estação de trabalho conectada à Internet</span><span class="sxs-lookup"><span data-stu-id="74cba-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="74cba-171">Para a primeira etapa, Olá procedimentos a seguir em sua estação de trabalho é toohello conectado à Internet.</span><span class="sxs-lookup"><span data-stu-id="74cba-171">For this first step, do hello following procedures on your workstation that is connected toohello Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="74cba-172">Etapa 1.1: Instalar o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="74cba-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="74cba-173">De saudação conectada à Internet estação de trabalho, baixe e instale o módulo do PowerShell do Azure Olá que inclui Olá cmdlets toomanage Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="74cba-173">From hello Internet-connected workstation, download and install hello Azure PowerShell module that includes hello cmdlets toomanage Azure Key Vault.</span></span> <span data-ttu-id="74cba-174">Isso requer uma versão mínima do 0.8.13.</span><span class="sxs-lookup"><span data-stu-id="74cba-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="74cba-175">Para obter instruções de instalação, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="74cba-175">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="74cba-176">Etapa 1.2: Obter a sua ID da assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="74cba-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="74cba-177">Iniciar uma sessão do PowerShell do Azure e entrar tooyour conta do Azure usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="74cba-177">Start an Azure PowerShell session and sign in tooyour Azure account by using hello following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="74cba-178">Na janela de pop-up do navegador hello, insira seu nome de usuário da conta do Azure e a senha.</span><span class="sxs-lookup"><span data-stu-id="74cba-178">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="74cba-179">Em seguida, use Olá [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) comando:</span><span class="sxs-lookup"><span data-stu-id="74cba-179">Then, use hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="74cba-180">Da saída de hello, localize a ID de Olá para assinatura Olá que você usará para o Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="74cba-180">From hello output, locate hello ID for hello subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="74cba-181">Você precisará dessa ID da assinatura mais tarde.</span><span class="sxs-lookup"><span data-stu-id="74cba-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="74cba-182">Não feche a janela do PowerShell do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="74cba-182">Do not close hello Azure PowerShell window.</span></span>

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="74cba-183">Etapa 1.3: Baixar Olá conjunto de ferramentas BYOK para Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="74cba-183">Step 1.3: Download hello BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="74cba-184">Vá toohello Microsoft Download Center e [baixar o conjunto de ferramentas do BYOK do Cofre de chaves do Azure Olá](http://www.microsoft.com/download/details.aspx?id=45345) para sua região ou instância do Azure.</span><span class="sxs-lookup"><span data-stu-id="74cba-184">Go toohello Microsoft Download Center and [download hello Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="74cba-185">Use os seguintes Olá toodownload de nome de pacote do informações tooidentify hello e seu correspondente SHA-256 hash do pacote:</span><span class="sxs-lookup"><span data-stu-id="74cba-185">Use hello following information tooidentify hello package name toodownload and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="74cba-186">**Estados Unidos:**</span><span class="sxs-lookup"><span data-stu-id="74cba-186">**United States:**</span></span>

<span data-ttu-id="74cba-187">KeyVault-BYOK-Tools-UnitedStates.zip</span><span class="sxs-lookup"><span data-stu-id="74cba-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="74cba-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="74cba-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="74cba-189">**Europa:**</span><span class="sxs-lookup"><span data-stu-id="74cba-189">**Europe:**</span></span>

<span data-ttu-id="74cba-190">KeyVault-BYOK-Tools-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="74cba-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="74cba-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="74cba-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="74cba-192">**Ásia:**</span><span class="sxs-lookup"><span data-stu-id="74cba-192">**Asia:**</span></span>

<span data-ttu-id="74cba-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="74cba-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="74cba-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="74cba-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="74cba-195">**América Latina:**</span><span class="sxs-lookup"><span data-stu-id="74cba-195">**Latin America:**</span></span>

<span data-ttu-id="74cba-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="74cba-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="74cba-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="74cba-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="74cba-198">**Japão:**</span><span class="sxs-lookup"><span data-stu-id="74cba-198">**Japan:**</span></span>

<span data-ttu-id="74cba-199">KeyVault-BYOK-Tools-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="74cba-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="74cba-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="74cba-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="74cba-201">**Coreia:**</span><span class="sxs-lookup"><span data-stu-id="74cba-201">**Korea:**</span></span>

<span data-ttu-id="74cba-202">KeyVault-BYOK-Tools-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="74cba-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="74cba-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="74cba-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="74cba-204">**Austrália:**</span><span class="sxs-lookup"><span data-stu-id="74cba-204">**Australia:**</span></span>

<span data-ttu-id="74cba-205">KeyVault-BYOK-Tools-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="74cba-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="74cba-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="74cba-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="74cba-207">**Azure Government:**</span><span class="sxs-lookup"><span data-stu-id="74cba-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="74cba-208">KeyVault-BYOK-Tools-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="74cba-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="74cba-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="74cba-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="74cba-210">**US Government DoD:**</span><span class="sxs-lookup"><span data-stu-id="74cba-210">**US Government DOD:**</span></span>

<span data-ttu-id="74cba-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="74cba-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="74cba-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="74cba-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="74cba-213">**Canadá:**</span><span class="sxs-lookup"><span data-stu-id="74cba-213">**Canada:**</span></span>

<span data-ttu-id="74cba-214">KeyVault-BYOK-Tools-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="74cba-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="74cba-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="74cba-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="74cba-216">**Alemanha:**</span><span class="sxs-lookup"><span data-stu-id="74cba-216">**Germany:**</span></span>

<span data-ttu-id="74cba-217">KeyVault-BYOK-Tools-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="74cba-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="74cba-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="74cba-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="74cba-219">**Índia:**</span><span class="sxs-lookup"><span data-stu-id="74cba-219">**India:**</span></span>

<span data-ttu-id="74cba-220">KeyVault-BYOK-Tools-India.zip</span><span class="sxs-lookup"><span data-stu-id="74cba-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="74cba-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="74cba-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="74cba-222">**Reino Unido:**</span><span class="sxs-lookup"><span data-stu-id="74cba-222">**United Kingdom:**</span></span>

<span data-ttu-id="74cba-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="74cba-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="74cba-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="74cba-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="74cba-225">integridade de saudação toovalidate de seu download conjunto de ferramentas BYOK, de sua sessão do PowerShell do Azure, use Olá [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="74cba-225">toovalidate hello integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="74cba-226">conjunto de ferramentas de saudação inclui o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="74cba-226">hello toolset includes hello following:</span></span>

* <span data-ttu-id="74cba-227">Um pacote de Chave de Troca de Chave (KEK) que tem um nome que começa com **BYOK-KEK-pkg-.**</span><span class="sxs-lookup"><span data-stu-id="74cba-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="74cba-228">Um pacote de Universo de Segurança que tem um nome que começa com **BYOK-SecurityWorld-pkg-.**</span><span class="sxs-lookup"><span data-stu-id="74cba-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="74cba-229">Um script do Python chamado **verifykeypackage.py.**</span><span class="sxs-lookup"><span data-stu-id="74cba-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="74cba-230">Um arquivo executável de linha de comando chamado **KeyTransferRemote.exe** e DLLs associadas.</span><span class="sxs-lookup"><span data-stu-id="74cba-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="74cba-231">Um pacote redistribuível do Visual C++, chamado **vcredist_x64.exe.**</span><span class="sxs-lookup"><span data-stu-id="74cba-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="74cba-232">Copie a unidade do hello pacote tooa USB ou outro armazenamento portátil.</span><span class="sxs-lookup"><span data-stu-id="74cba-232">Copy hello package tooa USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="74cba-233">Etapa 2: preparar sua estação de trabalho desconectada</span><span class="sxs-lookup"><span data-stu-id="74cba-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="74cba-234">Para essa segunda etapa, Olá seguindo os procedimentos na estação de trabalho de saudação que não está conectado tooa rede (Olá Internet ou sua rede interna).</span><span class="sxs-lookup"><span data-stu-id="74cba-234">For this second step, do hello following procedures on hello workstation that is not connected tooa network (either hello Internet or your internal network).</span></span>

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="74cba-235">Etapa 2.1: Preparar Olá desconectado de estação de trabalho com HSM da Thales</span><span class="sxs-lookup"><span data-stu-id="74cba-235">Step 2.1: Prepare hello disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="74cba-236">Instalar o software de suporte nCipher (Thales) hello em um computador Windows e anexe um computador de toothat HSM da Thales.</span><span class="sxs-lookup"><span data-stu-id="74cba-236">Install hello nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM toothat computer.</span></span>

<span data-ttu-id="74cba-237">Certifique-se de que Olá ferramentas Thales estão no caminho (**%nfast_home%\bin**).</span><span class="sxs-lookup"><span data-stu-id="74cba-237">Ensure that hello Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="74cba-238">Por exemplo, digite o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="74cba-238">For example, type hello following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="74cba-239">Para obter mais informações, consulte o guia do usuário de saudação incluído com hello HSM da Thales.</span><span class="sxs-lookup"><span data-stu-id="74cba-239">For more information, see hello user guide included with hello Thales HSM.</span></span>

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a><span data-ttu-id="74cba-240">Etapa 2.2: Conjunto de ferramentas Install Olá BYOK na estação de trabalho Olá desconectado</span><span class="sxs-lookup"><span data-stu-id="74cba-240">Step 2.2: Install hello BYOK toolset on hello disconnected workstation</span></span>
<span data-ttu-id="74cba-241">Copie o pacote de conjunto de ferramentas do BYOK de saudação da unidade do hello USB ou outro armazenamento portátil e, em seguida, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="74cba-241">Copy hello BYOK toolset package from hello USB drive or other portable storage, and then do hello following:</span></span>

1. <span data-ttu-id="74cba-242">Extrai arquivos de saudação do pacote de saudação baixada em qualquer pasta.</span><span class="sxs-lookup"><span data-stu-id="74cba-242">Extract hello files from hello downloaded package into any folder.</span></span>
2. <span data-ttu-id="74cba-243">Nessa pasta, execute o vcredist_x64.exe.</span><span class="sxs-lookup"><span data-stu-id="74cba-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="74cba-244">Siga as instruções de saudação toohello instalar componentes de tempo de execução do Visual C++ Olá para Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="74cba-244">Follow hello instructions toohello install hello Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="74cba-245">Etapa 3: Gerar a sua chave</span><span class="sxs-lookup"><span data-stu-id="74cba-245">Step 3: Generate your key</span></span>
<span data-ttu-id="74cba-246">Para a terceira etapa, Olá procedimentos a seguir na estação de trabalho Olá desconectado.</span><span class="sxs-lookup"><span data-stu-id="74cba-246">For this third step, do hello following procedures on hello disconnected workstation.</span></span> <span data-ttu-id="74cba-247">toocomplete essa etapa de seu HSM deve estar no modo de inicialização.</span><span class="sxs-lookup"><span data-stu-id="74cba-247">toocomplete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-hello-hsm-mode-tooi"></a><span data-ttu-id="74cba-248">Etapa 3.1: Alterar Olá HSM modo too'I'</span><span class="sxs-lookup"><span data-stu-id="74cba-248">Step 3.1: Change hello HSM mode too'I'</span></span>
<span data-ttu-id="74cba-249">Se você estiver usando Thales nShield borda, modo de saudação toochange: 1.</span><span class="sxs-lookup"><span data-stu-id="74cba-249">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="74cba-250">Use Olá modo botão toohighlight Olá modo necessário.</span><span class="sxs-lookup"><span data-stu-id="74cba-250">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="74cba-251">2.</span><span class="sxs-lookup"><span data-stu-id="74cba-251">2.</span></span> <span data-ttu-id="74cba-252">Em alguns segundos, pressione e segure o botão Limpar Olá para alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="74cba-252">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="74cba-253">Se o modo de saudação for alterado, Olá novo modo para de LED piscando e permanece aceso.</span><span class="sxs-lookup"><span data-stu-id="74cba-253">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="74cba-254">Olá LED de Status pode flash irregular por alguns segundos e, em seguida, pisca regularmente quando o dispositivo hello está pronto.</span><span class="sxs-lookup"><span data-stu-id="74cba-254">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="74cba-255">Caso contrário, a saudação dispositivo permanece no modo atual hello, com o modo apropriado de saudação LED aceso.</span><span class="sxs-lookup"><span data-stu-id="74cba-255">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="74cba-256">Etapa 3.2: Criar um universo de segurança</span><span class="sxs-lookup"><span data-stu-id="74cba-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="74cba-257">Inicie um prompt de comando e execute Olá programa do novo mundo Thales.</span><span class="sxs-lookup"><span data-stu-id="74cba-257">Start a command prompt and run hello Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="74cba-258">Este programa cria um **mundo de segurança** arquivo % NFAST_KMDATA%\local\world, que corresponde a toohello C:\ProgramData\nCipher\Key Management Data\local pasta.</span><span class="sxs-lookup"><span data-stu-id="74cba-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds toohello C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="74cba-259">Você pode usar valores diferentes para quorum hello, mas no nosso exemplo, você está tooenter solicitadas três cartões e em branco pins para cada um.</span><span class="sxs-lookup"><span data-stu-id="74cba-259">You can use different values for hello quorum but in our example, you’re prompted tooenter three blank cards and pins for each one.</span></span> <span data-ttu-id="74cba-260">Em seguida, os dois cartões oferecem mundo de segurança toohello acesso completo.</span><span class="sxs-lookup"><span data-stu-id="74cba-260">Then, any two cards give full access toohello security world.</span></span> <span data-ttu-id="74cba-261">Esses cartões se tornam Olá **conjunto de cartões de administrador** para Olá mundo de segurança novo.</span><span class="sxs-lookup"><span data-stu-id="74cba-261">These cards become hello **Administrator Card Set** for hello new security world.</span></span>

<span data-ttu-id="74cba-262">Em seguida, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="74cba-262">Then do hello following:</span></span>

* <span data-ttu-id="74cba-263">Fazer backup de arquivo do hello world.</span><span class="sxs-lookup"><span data-stu-id="74cba-263">Back up hello world file.</span></span> <span data-ttu-id="74cba-264">Proteger e proteger o arquivo do Olá mundo, Olá cartões de administrador e seus pins e certifique-se de que ninguém tenha acesso toomore que um cartão.</span><span class="sxs-lookup"><span data-stu-id="74cba-264">Secure and protect hello world file, hello Administrator Cards, and their pins, and make sure that no single person has access toomore than one card.</span></span>

### <a name="step-33-change-hello-hsm-mode-tooo"></a><span data-ttu-id="74cba-265">Etapa 3.3: Alterar Olá HSM modo too'O'</span><span class="sxs-lookup"><span data-stu-id="74cba-265">Step 3.3: Change hello HSM mode too'O'</span></span>
<span data-ttu-id="74cba-266">Se você estiver usando Thales nShield borda, modo de saudação toochange: 1.</span><span class="sxs-lookup"><span data-stu-id="74cba-266">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="74cba-267">Use Olá modo botão toohighlight Olá modo necessário.</span><span class="sxs-lookup"><span data-stu-id="74cba-267">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="74cba-268">2.</span><span class="sxs-lookup"><span data-stu-id="74cba-268">2.</span></span> <span data-ttu-id="74cba-269">Em alguns segundos, pressione e segure o botão Limpar Olá para alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="74cba-269">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="74cba-270">Se o modo de saudação for alterado, Olá novo modo para de LED piscando e permanece aceso.</span><span class="sxs-lookup"><span data-stu-id="74cba-270">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="74cba-271">Olá LED de Status pode flash irregular por alguns segundos e, em seguida, pisca regularmente quando o dispositivo hello está pronto.</span><span class="sxs-lookup"><span data-stu-id="74cba-271">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="74cba-272">Caso contrário, a saudação dispositivo permanece no modo atual hello, com o modo apropriado de saudação LED aceso.</span><span class="sxs-lookup"><span data-stu-id="74cba-272">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>


### <a name="step-34-validate-hello-downloaded-package"></a><span data-ttu-id="74cba-273">Etapa 3.4: Validar o pacote de saudação baixada</span><span class="sxs-lookup"><span data-stu-id="74cba-273">Step 3.4: Validate hello downloaded package</span></span>
<span data-ttu-id="74cba-274">Esta etapa é opcional mas recomendado para que você possa validar a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="74cba-274">This step is optional but recommended so that you can validate hello following:</span></span>

* <span data-ttu-id="74cba-275">Olá chave de troca de chave que está incluído no conjunto de ferramentas Olá foi gerada de um Thales HSM genuíno.</span><span class="sxs-lookup"><span data-stu-id="74cba-275">hello Key Exchange Key that is included in hello toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="74cba-276">hash de saudação do Olá mundo de segurança que está incluído no conjunto de ferramentas Olá foi gerada em um Thales HSM genuíno.</span><span class="sxs-lookup"><span data-stu-id="74cba-276">hello hash of hello Security World that is included in hello toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="74cba-277">Olá Key Exchange Key é não exportável.</span><span class="sxs-lookup"><span data-stu-id="74cba-277">hello Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="74cba-278">Olá toovalidate baixado o pacote, hello HSM deve estar conectado, ligado e deve ter um mundo de segurança nele (como Olá um que você acabou de criar).</span><span class="sxs-lookup"><span data-stu-id="74cba-278">toovalidate hello downloaded package, hello HSM must be connected, powered on, and must have a security world on it (such as hello one you’ve just created).</span></span>
>
>

<span data-ttu-id="74cba-279">pacote de saudação baixada toovalidate:</span><span class="sxs-lookup"><span data-stu-id="74cba-279">toovalidate hello downloaded package:</span></span>

1. <span data-ttu-id="74cba-280">Execute Olá script verifykeypackage.py digitando uma das seguintes hello, dependendo da sua região ou instância do Azure:</span><span class="sxs-lookup"><span data-stu-id="74cba-280">Run hello verifykeypackage.py script by typing one of hello following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="74cba-281">Para a América do Norte:</span><span class="sxs-lookup"><span data-stu-id="74cba-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="74cba-282">Para a Europa:</span><span class="sxs-lookup"><span data-stu-id="74cba-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="74cba-283">Para a Ásia:</span><span class="sxs-lookup"><span data-stu-id="74cba-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="74cba-284">Para a América Latina:</span><span class="sxs-lookup"><span data-stu-id="74cba-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="74cba-285">Para o Japão:</span><span class="sxs-lookup"><span data-stu-id="74cba-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="74cba-286">Para a Coreia:</span><span class="sxs-lookup"><span data-stu-id="74cba-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="74cba-287">Para a Austrália:</span><span class="sxs-lookup"><span data-stu-id="74cba-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="74cba-288">Para [Azure Government](https://azure.microsoft.com/features/gov/), que usa a instância do governo Olá dos EUA do Azure:</span><span class="sxs-lookup"><span data-stu-id="74cba-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="74cba-289">Para US Government DoD:</span><span class="sxs-lookup"><span data-stu-id="74cba-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="74cba-290">Para o Canadá:</span><span class="sxs-lookup"><span data-stu-id="74cba-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="74cba-291">Para a Alemanha:</span><span class="sxs-lookup"><span data-stu-id="74cba-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="74cba-292">Para a Índia:</span><span class="sxs-lookup"><span data-stu-id="74cba-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="74cba-293">Olá software Thales inclui python em %NFAST_HOME%\python\bin</span><span class="sxs-lookup"><span data-stu-id="74cba-293">hello Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="74cba-294">Confirme que você vê Olá seguinte, que indica a validação bem-sucedida: **resultado: êxito**</span><span class="sxs-lookup"><span data-stu-id="74cba-294">Confirm that you see hello following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="74cba-295">Este script valida a cadeia do assinante Olá backup toohello chave raiz Thales.</span><span class="sxs-lookup"><span data-stu-id="74cba-295">This script validates hello signer chain up toohello Thales root key.</span></span> <span data-ttu-id="74cba-296">Olá hash dessa chave raiz está inserido no script hello e seu valor deve ser **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span><span class="sxs-lookup"><span data-stu-id="74cba-296">hello hash of this root key is embedded in hello script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="74cba-297">Você também pode confirmar esse valor separadamente visitando Olá [site da Thales](http://www.thalesesec.com/).</span><span class="sxs-lookup"><span data-stu-id="74cba-297">You can also confirm this value separately by visiting hello [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="74cba-298">Agora você está pronto toocreate uma nova chave.</span><span class="sxs-lookup"><span data-stu-id="74cba-298">You’re now ready toocreate a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="74cba-299">Etapa 3.5: Criar uma nova chave</span><span class="sxs-lookup"><span data-stu-id="74cba-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="74cba-300">Gerar uma chave usando Olá Thales **generatekey** programa.</span><span class="sxs-lookup"><span data-stu-id="74cba-300">Generate a key by using hello Thales **generatekey** program.</span></span>

<span data-ttu-id="74cba-301">Execute Olá chave de saudação do toogenerate de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="74cba-301">Run hello following command toogenerate hello key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="74cba-302">Quando você executar esse comando, use estas instruções:</span><span class="sxs-lookup"><span data-stu-id="74cba-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="74cba-303">Olá parâmetro *proteger* deve ser definido como o valor de toohello **módulo**, conforme mostrado.</span><span class="sxs-lookup"><span data-stu-id="74cba-303">hello parameter *protect* must be set toohello value **module**, as shown.</span></span> <span data-ttu-id="74cba-304">Isso cria uma chave protegida pelo módulo.</span><span class="sxs-lookup"><span data-stu-id="74cba-304">This creates a module-protected key.</span></span> <span data-ttu-id="74cba-305">Olá conjunto de ferramentas BYOK não dá suporte a chaves protegidas por OCS.</span><span class="sxs-lookup"><span data-stu-id="74cba-305">hello BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="74cba-306">Substituir valor de saudação do *contosokey* para Olá **ident** e **plainname** com qualquer valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="74cba-306">Replace hello value of *contosokey* for hello **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="74cba-307">custos administrativos toominimize e reduzir o risco de saudação de erros, recomendamos que você use Olá mesmo valor para ambos.</span><span class="sxs-lookup"><span data-stu-id="74cba-307">toominimize administrative overheads and reduce hello risk of errors, we recommend that you use hello same value for both.</span></span> <span data-ttu-id="74cba-308">Olá **ident** valor deve conter somente números, traços, letras maiusculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="74cba-308">hello **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="74cba-309">Olá pubexp é deixado em branco (padrão) neste exemplo, mas você pode especificar valores específicos.</span><span class="sxs-lookup"><span data-stu-id="74cba-309">hello pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="74cba-310">Para obter mais informações, consulte Olá documentação da Thales.</span><span class="sxs-lookup"><span data-stu-id="74cba-310">For more information, see hello Thales documentation.</span></span>

<span data-ttu-id="74cba-311">Este comando cria um arquivo de chave de token na pasta %NFAST_KMDATA%\local com um nome iniciado por **key_simple _**, seguido pelo Olá **ident** que foi especificado no comando hello.</span><span class="sxs-lookup"><span data-stu-id="74cba-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by hello **ident** that was specified in hello command.</span></span> <span data-ttu-id="74cba-312">Por exemplo: **key_simple_contosokey**.</span><span class="sxs-lookup"><span data-stu-id="74cba-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="74cba-313">Esse arquivo contém uma chave criptografada.</span><span class="sxs-lookup"><span data-stu-id="74cba-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="74cba-314">Faça backup deste arquivo de Chave com Token em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="74cba-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74cba-315">Quando você transfere sua chave tooAzure Cofre de chaves posteriormente, o Microsoft não poderá exportar esta chave tooyou back por é extremamente importante que você faça backup do seu mundo de segurança e de chave com segurança.</span><span class="sxs-lookup"><span data-stu-id="74cba-315">When you later transfer your key tooAzure Key Vault, Microsoft cannot export this key back tooyou so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="74cba-316">Entre em contato com a Thales para obter orientação e as práticas recomendadas para fazer backup da sua chave.</span><span class="sxs-lookup"><span data-stu-id="74cba-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="74cba-317">Você é agora pronto tootransfer sua chave tooAzure Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="74cba-317">You are now ready tootransfer your key tooAzure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="74cba-318">Etapa 4: Preparar a sua chave para transferência</span><span class="sxs-lookup"><span data-stu-id="74cba-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="74cba-319">Para esta etapa quarta, Olá procedimentos a seguir na estação de trabalho Olá desconectado.</span><span class="sxs-lookup"><span data-stu-id="74cba-319">For this fourth step, do hello following procedures on hello disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="74cba-320">Etapa 4.1: Criar uma cópia da chave com permissões reduzidas</span><span class="sxs-lookup"><span data-stu-id="74cba-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="74cba-321">Abra um prompt de comando novo e alterar Olá atual toohello local do diretório onde você descompactou o arquivo zip do hello BYOK.</span><span class="sxs-lookup"><span data-stu-id="74cba-321">Open a new command prompt and change hello current directory toohello location where you unzipped hello BYOK zip file.</span></span> <span data-ttu-id="74cba-322">permissões de saudação tooreduce em sua chave, em um prompt de comando, execute um dos seguintes hello, dependendo da sua região ou instância do Azure:</span><span class="sxs-lookup"><span data-stu-id="74cba-322">tooreduce hello permissions on your key, from a command prompt, run one of hello following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="74cba-323">Para a América do Norte:</span><span class="sxs-lookup"><span data-stu-id="74cba-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="74cba-324">Para a Europa:</span><span class="sxs-lookup"><span data-stu-id="74cba-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="74cba-325">Para a Ásia:</span><span class="sxs-lookup"><span data-stu-id="74cba-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="74cba-326">Para a América Latina:</span><span class="sxs-lookup"><span data-stu-id="74cba-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="74cba-327">Para o Japão:</span><span class="sxs-lookup"><span data-stu-id="74cba-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="74cba-328">Para a Coreia:</span><span class="sxs-lookup"><span data-stu-id="74cba-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="74cba-329">Para a Austrália:</span><span class="sxs-lookup"><span data-stu-id="74cba-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="74cba-330">Para [Azure Government](https://azure.microsoft.com/features/gov/), que usa a instância do governo Olá dos EUA do Azure:</span><span class="sxs-lookup"><span data-stu-id="74cba-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="74cba-331">Para US Government DoD:</span><span class="sxs-lookup"><span data-stu-id="74cba-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="74cba-332">Para o Canadá:</span><span class="sxs-lookup"><span data-stu-id="74cba-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="74cba-333">Para a Alemanha:</span><span class="sxs-lookup"><span data-stu-id="74cba-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="74cba-334">Para a Índia:</span><span class="sxs-lookup"><span data-stu-id="74cba-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="74cba-335">Quando você executa esse comando, substitua *contosokey* com hello mesmo valor especificado em **3.5 etapa: criar uma nova chave** de saudação [gerar sua chave](#step-3-generate-your-key) etapa.</span><span class="sxs-lookup"><span data-stu-id="74cba-335">When you run this command, replace *contosokey* with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="74cba-336">Você será solicitado a tooplug seus cartões de administrador do mundo de segurança.</span><span class="sxs-lookup"><span data-stu-id="74cba-336">You are asked tooplug in your security world admin cards.</span></span>

<span data-ttu-id="74cba-337">Quando Olá comando for concluído, você verá **resultado: êxito** e cópia de saudação da sua chave com permissões reduzidas são no arquivo hello chamado key_xferacid _<contosokey>.</span><span class="sxs-lookup"><span data-stu-id="74cba-337">When hello command completes, you see **Result: SUCCESS** and hello copy of your key with reduced permissions are in hello file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="74cba-338">Pode inspeciona Olá ACLS usando o seguinte comandos usando Olá utilitários Thales:</span><span class="sxs-lookup"><span data-stu-id="74cba-338">You may inspects hello ACLS using following commands using hello Thales utilities:</span></span>

* <span data-ttu-id="74cba-339">aclprint.py:</span><span class="sxs-lookup"><span data-stu-id="74cba-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="74cba-340">kmfile-dump.exe:</span><span class="sxs-lookup"><span data-stu-id="74cba-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="74cba-341">Quando você executar esses comandos, substitua contosokey Olá mesmo valor especificado em **3.5 etapa: criar uma nova chave** de saudação [gerar sua chave](#step-3-generate-your-key) etapa.</span><span class="sxs-lookup"><span data-stu-id="74cba-341">When you run these commands, replace contosokey with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="74cba-342">Etapa 4.2: Criptografar a chave usando a Chave de Troca de Chaves da Microsoft</span><span class="sxs-lookup"><span data-stu-id="74cba-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="74cba-343">Execute um dos Olá comandos, dependendo da sua região ou instância do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="74cba-343">Run one of hello following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="74cba-344">Para a América do Norte:</span><span class="sxs-lookup"><span data-stu-id="74cba-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="74cba-345">Para a Europa:</span><span class="sxs-lookup"><span data-stu-id="74cba-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="74cba-346">Para a Ásia:</span><span class="sxs-lookup"><span data-stu-id="74cba-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="74cba-347">Para a América Latina:</span><span class="sxs-lookup"><span data-stu-id="74cba-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="74cba-348">Para o Japão:</span><span class="sxs-lookup"><span data-stu-id="74cba-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="74cba-349">Para a Coreia:</span><span class="sxs-lookup"><span data-stu-id="74cba-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="74cba-350">Para a Austrália:</span><span class="sxs-lookup"><span data-stu-id="74cba-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="74cba-351">Para [Azure Government](https://azure.microsoft.com/features/gov/), que usa a instância do governo Olá dos EUA do Azure:</span><span class="sxs-lookup"><span data-stu-id="74cba-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="74cba-352">Para US Government DoD:</span><span class="sxs-lookup"><span data-stu-id="74cba-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="74cba-353">Para o Canadá:</span><span class="sxs-lookup"><span data-stu-id="74cba-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="74cba-354">Para a Alemanha:</span><span class="sxs-lookup"><span data-stu-id="74cba-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="74cba-355">Para a Índia:</span><span class="sxs-lookup"><span data-stu-id="74cba-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="74cba-356">Quando você executar esse comando, use estas instruções:</span><span class="sxs-lookup"><span data-stu-id="74cba-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="74cba-357">Substituir *contosokey* com identificador de saudação que é usado como chave de saudação toogenerate em **3.5 etapa: criar uma nova chave** de saudação [gerar sua chave](#step-3-generate-your-key) etapa.</span><span class="sxs-lookup"><span data-stu-id="74cba-357">Replace *contosokey* with hello identifier that you used toogenerate hello key in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="74cba-358">Substituir *SubscriptionID* com ID Olá Olá assinatura do Azure que contém seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="74cba-358">Replace *SubscriptionID* with hello ID of hello Azure subscription that contains your key vault.</span></span> <span data-ttu-id="74cba-359">Esse valor foi recuperado anteriormente, em **etapa 1.2: Obtenha sua ID de assinatura do Azure** de saudação [preparar sua estação de trabalho conectada à Internet](#step-1-prepare-your-internet-connected-workstation) etapa.</span><span class="sxs-lookup"><span data-stu-id="74cba-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from hello [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="74cba-360">Substitua *ContosoFirstHSMKey* por um rótulo que seja usado para o nome do arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="74cba-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="74cba-361">Quando isso for concluído com êxito, ele exibe **resultado: êxito** e há um novo arquivo na pasta atual Olá tem Olá nome a seguir: KeyTransferPackage -*ContosoFirstHSMkey*. byok</span><span class="sxs-lookup"><span data-stu-id="74cba-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in hello current folder that has hello following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a><span data-ttu-id="74cba-362">Etapa 4.3: Copiar a transferência de chave pacote toohello conectada à Internet estação de trabalho</span><span class="sxs-lookup"><span data-stu-id="74cba-362">Step 4.3: Copy your key transfer package toohello Internet-connected workstation</span></span>
<span data-ttu-id="74cba-363">Use uma unidade USB ou outro arquivo de saída do armazenamento portátil toocopy Olá de saudação anterior (KeyTransferPackage-ContosoFirstHSMkey.byok) da etapa tooyour conectada à Internet estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="74cba-363">Use a USB drive or other portable storage toocopy hello output file from hello previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a><span data-ttu-id="74cba-364">Etapa 5: Transferir sua chave tooAzure Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="74cba-364">Step 5: Transfer your key tooAzure Key Vault</span></span>
<span data-ttu-id="74cba-365">Para essa etapa final, Olá conectada à Internet estação de trabalho, use Olá [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload Olá chave pacote de transferência que você copiou da saudação desconectado toohello de estação de trabalho HSM do Cofre de chaves do Azure:</span><span class="sxs-lookup"><span data-stu-id="74cba-365">For this final step, on hello Internet-connected workstation, use hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello key transfer package that you copied from hello disconnected workstation toohello Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="74cba-366">Se Olá upload for bem-sucedido, você verá propriedades Olá exibido da chave de saudação que você acabou de adicionar.</span><span class="sxs-lookup"><span data-stu-id="74cba-366">If hello upload is successful, you see displayed hello properties of hello key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74cba-367">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74cba-367">Next steps</span></span>
<span data-ttu-id="74cba-368">Agora você pode usar essa chave de HSM protegido no Cofre da Chave.</span><span class="sxs-lookup"><span data-stu-id="74cba-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="74cba-369">Para obter mais informações, consulte Olá **se você quiser que um módulo de segurança de hardware (HSM) de toouse** seção Olá [guia de Introdução ao Azure Key Vault](key-vault-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="74cba-369">For more information, see hello **If you want toouse a hardware security module (HSM)** section in hello [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
