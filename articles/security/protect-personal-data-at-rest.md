---
title: aaaAzure proteger os dados pessoais em repouso com criptografia | Microsoft Docs
description: "Este artigo faz parte de uma série de ajudá-lo a usar dados pessoais tooprotect do Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a><span data-ttu-id="03249-103">Tecnologias de criptografia do Azure: proteger dados pessoais em repouso com criptografia</span><span class="sxs-lookup"><span data-stu-id="03249-103">Azure encryption technologies: Protect personal data at rest with encryption</span></span>

<span data-ttu-id="03249-104">Este artigo ajuda você a entender e usar dados de toosecure de tecnologias de criptografia do Azure em repouso.</span><span class="sxs-lookup"><span data-stu-id="03249-104">This article helps you understand and use Azure encryption technologies toosecure data at rest.</span></span>

<span data-ttu-id="03249-105">Criptografia de dados em repouso é essencial como um melhor prática tooprotect dados confidenciais ou pessoais e toomeet conformidade e requisitos de privacidade de dados.</span><span class="sxs-lookup"><span data-stu-id="03249-105">Encryption of data at rest is essential as a best practice tooprotect sensitive or personal data and toomeet compliance and data privacy requirements.</span></span>
<span data-ttu-id="03249-106">Criptografia em repouso é projetado tooprevent invasor de saudação acessem dados descriptografado de saudação assegurando Olá dados são criptografados quando no disco.</span><span class="sxs-lookup"><span data-stu-id="03249-106">Encryption at rest is designed tooprevent hello attacker from accessing hello unencrypted data by ensuring hello data is encrypted when on disk.</span></span>

## <a name="scenario"></a><span data-ttu-id="03249-107">Cenário</span><span class="sxs-lookup"><span data-stu-id="03249-107">Scenario</span></span> 

<span data-ttu-id="03249-108">Uma empresa cruzeiro grandes, com sede em Olá Estados Unidos, está expandindo suas roteiros de toooffer operações Olá Mediterrâneo e mares báltico, bem como Olá Britânicas.</span><span class="sxs-lookup"><span data-stu-id="03249-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="03249-109">toosupport os esforços adquiriu várias linhas de cruzeiro menores com base na Itália, Alemanha, Dinamarca e Olá Reino Unido</span><span class="sxs-lookup"><span data-stu-id="03249-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="03249-110">empresa de saudação usa dados corporativos do Microsoft Azure toostore na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="03249-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="03249-111">Isso pode incluir funcionário e/ou informações do cliente, como:</span><span class="sxs-lookup"><span data-stu-id="03249-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="03249-112">endereços</span><span class="sxs-lookup"><span data-stu-id="03249-112">addresses</span></span>
- <span data-ttu-id="03249-113">números de telefone</span><span class="sxs-lookup"><span data-stu-id="03249-113">phone numbers</span></span>
- <span data-ttu-id="03249-114">números de identificação fiscal</span><span class="sxs-lookup"><span data-stu-id="03249-114">tax identification numbers</span></span>
- <span data-ttu-id="03249-115">informações de médicas</span><span class="sxs-lookup"><span data-stu-id="03249-115">medical information</span></span>
- <span data-ttu-id="03249-116">informações de cartão de crédito</span><span class="sxs-lookup"><span data-stu-id="03249-116">credit card information</span></span>

<span data-ttu-id="03249-117">empresa Olá deve proteger a privacidade de Olá do funcionário e dados do cliente ao fazer departamentos toothose acessível de dados que precisam dela.</span><span class="sxs-lookup"><span data-stu-id="03249-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="03249-118">(como departamentos de folha de pagamento e reservas)</span><span class="sxs-lookup"><span data-stu-id="03249-118">(such as payroll and reservations departments)</span></span>

<span data-ttu-id="03249-119">linha de cruzeiro Olá também mantém um banco de dados grande de membros do programa de recompensa e fidelidade que incluem informações pessoais tootrack relações com os clientes atuais e anteriores.</span><span class="sxs-lookup"><span data-stu-id="03249-119">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

### <a name="problem-statement"></a><span data-ttu-id="03249-120">Problema declarado</span><span class="sxs-lookup"><span data-stu-id="03249-120">Problem statement</span></span>

<span data-ttu-id="03249-121">empresa Olá deve proteger a privacidade de saudação dos dados pessoais dos funcionários e clientes ao fazer departamentos toothose acessível de dados que precisam dela (por exemplo, os departamentos de folha de pagamento e reservas).</span><span class="sxs-lookup"><span data-stu-id="03249-121">hello company must protect hello privacy of employees’ and customers’ personal data while making data accessible toothose departments that need it (such as payroll and reservations departments).</span></span> <span data-ttu-id="03249-122">Esses dados pessoais são armazenados fora do Centro de dados corporativos controlados hello e não está sob controle físico da empresa hello.</span><span class="sxs-lookup"><span data-stu-id="03249-122">This personal data is stored outside of hello corporate-controlled data center and is not under hello company’s physical control.</span></span>

### <a name="company-goal"></a><span data-ttu-id="03249-123">Meta da empresa</span><span class="sxs-lookup"><span data-stu-id="03249-123">Company goal</span></span>

<span data-ttu-id="03249-124">Como parte de uma estratégia de segurança em várias camadas de defesa em profundidade, é um tooensure de meta da empresa que todas as fontes de dados que contêm dados pessoais são criptografadas, incluindo aqueles que residem no armazenamento em nuvem.</span><span class="sxs-lookup"><span data-stu-id="03249-124">As part of a multi-layered defense-in-depth security strategy, it is a company goal tooensure that all data sources that contain personal data are encrypted, including those residing in cloud storage.</span></span> <span data-ttu-id="03249-125">Se não estiver autorizado pessoas ganho acessar toohello os dados pessoais, deve ser em um formulário que será renderizado ilegível.</span><span class="sxs-lookup"><span data-stu-id="03249-125">If unauthorized persons gain access toohello personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="03249-126">A aplicação da criptografia deve ser fácil ou transparente – para os usuários e administradores.</span><span class="sxs-lookup"><span data-stu-id="03249-126">Applying encryption should be easy, or transparent – for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="03249-127">Soluções</span><span class="sxs-lookup"><span data-stu-id="03249-127">Solutions</span></span>

<span data-ttu-id="03249-128">Os serviços do Azure fornecem vários toohelp ferramentas e tecnologias de proteger dados pessoais em repouso criptografando-os.</span><span class="sxs-lookup"><span data-stu-id="03249-128">Azure services provide multiple tools and technologies toohelp you protect personal data at rest by encrypting it.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="03249-129">Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="03249-129">Azure Key Vault</span></span>

<span data-ttu-id="03249-130">[Cofre de chaves do Azure](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) fornece armazenamento seguro para as chaves de saudação usadas tooencrypt dados em repouso em serviços do Azure e Olá recomenda solução de armazenamento e gerenciamento de chave.</span><span class="sxs-lookup"><span data-stu-id="03249-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) provides secure storage for hello keys used tooencrypt data at rest in Azure services and is hello recommended key storage and management solution.</span></span> <span data-ttu-id="03249-131">Gerenciamento de chaves de criptografia é essencial toosecuring armazenado dados.</span><span class="sxs-lookup"><span data-stu-id="03249-131">Encryption key management is essential toosecuring stored data.</span></span>

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a><span data-ttu-id="03249-132">Como usar as chaves de tooprotect do Cofre de chaves do Azure que criptografam dados pessoais?</span><span class="sxs-lookup"><span data-stu-id="03249-132">How do I use Azure Key Vault tooprotect keys that encrypt personal data?</span></span>

<span data-ttu-id="03249-133">toouse Cofre de chaves do Azure, você precisa de uma assinatura tooan conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="03249-133">toouse Azure Key Vault, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="03249-134">Você também precisa do Azure PowerShell instalado.</span><span class="sxs-lookup"><span data-stu-id="03249-134">You also need Azure PowerShell installed.</span></span> <span data-ttu-id="03249-135">As etapas incluem o uso de cmdlets do PowerShell, a seguir Olá toodo:</span><span class="sxs-lookup"><span data-stu-id="03249-135">Steps include using PowerShell cmdlets toodo hello following:</span></span>

1. <span data-ttu-id="03249-136">Conecte-se tooyour assinaturas</span><span class="sxs-lookup"><span data-stu-id="03249-136">Connect tooyour subscriptions</span></span>

2. <span data-ttu-id="03249-137">Criar um cofre de chave</span><span class="sxs-lookup"><span data-stu-id="03249-137">Create a key vault</span></span>

3. <span data-ttu-id="03249-138">Adicionar uma chave ou segredo toohello Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="03249-138">Add a key or secret toohello key vault</span></span>

4. <span data-ttu-id="03249-139">Registrar aplicativos que irá usar o Cofre de chaves Olá com Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="03249-139">Register applications that will use hello key vault with Azure Active Directory</span></span>

5. <span data-ttu-id="03249-140">Autorizar Olá aplicativos toouse Olá chave ou segredo</span><span class="sxs-lookup"><span data-stu-id="03249-140">Authorize hello applications toouse hello key or secret</span></span>

<span data-ttu-id="03249-141">toocreate um cofre de chaves, use Olá cmdlet do PowerShell New-AzureRmKeyVault.</span><span class="sxs-lookup"><span data-stu-id="03249-141">toocreate a key vault, use hello New-AzureRmKeyVault PowerShell CmDlt.</span></span> <span data-ttu-id="03249-142">Você atribuirá um nome de cofre, um nome do grupo de recursos e a localização geográfica.</span><span class="sxs-lookup"><span data-stu-id="03249-142">You will assign a vault name, resource group name, and geographic location.</span></span> <span data-ttu-id="03249-143">Você usará o nome do cofre hello quando o gerenciamento de chaves por meio de outros Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="03249-143">You’ll use hello vault name when managing keys via other Cmdlets.</span></span> <span data-ttu-id="03249-144">Aplicativos que usam o cofre Olá por meio da API REST de saudação usará o Cofre de saudação URI.</span><span class="sxs-lookup"><span data-stu-id="03249-144">Applications that use hello vault through hello REST API will use hello vault URI.</span></span>

<span data-ttu-id="03249-145">O Azure Key Vault pode fornecer uma chave protegida por software para você ou você pode importar uma chave existente em um arquivo .PFX.</span><span class="sxs-lookup"><span data-stu-id="03249-145">Azure Key Vault can provide a software-protected key for you, or you can import an existing key in a .PFX file.</span></span> <span data-ttu-id="03249-146">Você também pode armazenar segredos (senhas) no cofre hello.</span><span class="sxs-lookup"><span data-stu-id="03249-146">You can also store secrets (passwords) in hello vault.</span></span>

<span data-ttu-id="03249-147">Você também pode gerar uma chave no seu HSM local e transferi-la tooHSMs no hello serviço de Cofre de chaves sem chave Olá deixando o limite do HSM hello.</span><span class="sxs-lookup"><span data-stu-id="03249-147">You can also generate a key in your local HSM and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary.</span></span>

<span data-ttu-id="03249-148">Para obter instruções detalhadas sobre como usar o Cofre de chaves do Azure, siga as etapas em Olá [Introdução ao Cofre de chaves do Azure.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span><span class="sxs-lookup"><span data-stu-id="03249-148">For detailed instructions on using Azure Key Vault, follow hello steps in [Get Started with Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span></span>

<span data-ttu-id="03249-149">Para obter uma lista de Cmdlets do PowerShell usados com o Azure Key Vault, consulte [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="03249-149">For a list of PowerShell Cmdlets used with Azure Key Vault, see [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

### <a name="azure-disk-encryption-for-windows"></a><span data-ttu-id="03249-150">Azure Disk Encryption para o Windows</span><span class="sxs-lookup"><span data-stu-id="03249-150">Azure Disk Encryption for Windows</span></span>

<span data-ttu-id="03249-151">O [Azure Disk Encryption para VMs IaaS Windows e Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protege dados pessoais em repouso em máquinas virtuais do Azure e é integrado ao Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="03249-151">[Azure Disk Encryption for Windows and Linux IaaS VMs](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protects personal data at rest on Azure virtual machines and integrates with Azure Key Vault.</span></span> <span data-ttu-id="03249-152">Criptografia de disco do Azure usa [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) no Windows e [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) no Linux tooencrypt ambos Olá discos de dados do sistema operacional e hello.</span><span class="sxs-lookup"><span data-stu-id="03249-152">Azure Disk Encryption uses [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows and [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux tooencrypt both hello OS and hello data disks.</span></span> <span data-ttu-id="03249-153">Há suporte para o Azure Disk Encryption no Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 e nos clientes Windows 8 e Windows 10.</span><span class="sxs-lookup"><span data-stu-id="03249-153">Azure Disk Encryption is supported on Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, and on Windows 8 and Windows 10 clients.</span></span>

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a><span data-ttu-id="03249-154">Como usa os dados pessoais de tooprotect de criptografia de disco do Azure?</span><span class="sxs-lookup"><span data-stu-id="03249-154">How do I use Azure Disk Encryption tooprotect personal data?</span></span>

<span data-ttu-id="03249-155">toouse criptografia de disco do Azure, você precisa de uma assinatura tooan conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="03249-155">toouse Azure Disk Encryption, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="03249-156">Criptografia de disco de Azure tooenable para Windows e VMs do Linux, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="03249-156">tooenable Azure Disk Encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="03249-157">Usar o modelo do Gerenciador de recursos de criptografia de disco do Azure hello, PowerShell ou criptografia de disco de tooenable Olá interface de linha de comando (CLI) e especifique a configuração de criptografia.</span><span class="sxs-lookup"><span data-stu-id="03249-157">Use hello Azure Disk Encryption Resource Manager template, PowerShell, or hello command line interface (CLI) tooenable disk encryption and specify the  encryption configuration.</span></span> 

2. <span data-ttu-id="03249-158">Conceder acesso toohello plataforma Windows Azure tooread Olá material de criptografia do seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="03249-158">Grant access toohello Azure platform tooread hello encryption material from your key vault.</span></span>

3. <span data-ttu-id="03249-159">Forneça um Azure Active Directory (AAD) aplicativo identidade toowrite Olá criptografia tooyour material de chave Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="03249-159">Provide an Azure Active Directory (AAD) application identity toowrite hello encryption key material tooyour key vault.</span></span>

<span data-ttu-id="03249-160">Azure atualizar hello VM e configuração do Cofre de chaves hello e configurar sua VM criptografado.</span><span class="sxs-lookup"><span data-stu-id="03249-160">Azure will update hello VM and hello key vault configuration, and set up your encrypted VM.</span></span>

<span data-ttu-id="03249-161">Quando você configura seu Cofre de chaves de toosupport criptografia de disco do Azure, você pode adicionar uma chave de criptografia de chave (KEK) para maior segurança e toosupport backup de máquinas de virtuais criptografadas.</span><span class="sxs-lookup"><span data-stu-id="03249-161">When you set up your key vault toosupport Azure Disk Encryption, you can add a key encryption key (KEK) for added security and toosupport backup of encrypted virtual machines.</span></span>

![](media/protect-personal-data-at-rest/create-key.png)

<span data-ttu-id="03249-162">Instruções detalhadas para cenários de implantação específicos e as experiências do usuário são incluídas em [Azure Disk Encryption para VMs IaaS Windows e Linux.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span><span class="sxs-lookup"><span data-stu-id="03249-162">Detailed instructions for specific deployment scenarios and user experiences are included in [Azure Disk Encryption for Windows and Linux IaaS VMs.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span></span>

### <a name="azure-storage-service-encryption"></a><span data-ttu-id="03249-163">Criptografia do Serviço de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="03249-163">Azure Storage Service Encryption</span></span>

<span data-ttu-id="03249-164">[Azure Storage Service criptografia (SSE) para dados em repouso](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) ajuda a proteger e proteger seu dados toomeet seus compromissos de segurança e conformidade organizacionais.</span><span class="sxs-lookup"><span data-stu-id="03249-164">[Azure Storage Service Encryption (SSE) for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helps you protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="03249-165">Armazenamento do Azure automaticamente criptografa os dados usando toostorage de toopersisting anterior de criptografia de AES de 256 bits e a descriptografa tooretrieval anterior.</span><span class="sxs-lookup"><span data-stu-id="03249-165">Azure Storage automatically encrypts your data using 256-bit AES encryption prior toopersisting toostorage, and decrypts it prior tooretrieval.</span></span> <span data-ttu-id="03249-166">Esse serviço está disponível para Blobs e Arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="03249-166">This service is available for Azure Blobs and Files.</span></span>

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a><span data-ttu-id="03249-167">Como usa os dados pessoais de tooprotect de criptografia do serviço de armazenamento?</span><span class="sxs-lookup"><span data-stu-id="03249-167">How do I use Storage Service Encryption tooprotect personal data?</span></span>

<span data-ttu-id="03249-168">tooenable criptografia do serviço de armazenamento, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="03249-168">tooenable Storage Service Encryption, do hello following:</span></span>

1. <span data-ttu-id="03249-169">Faça logon no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="03249-169">Log into hello Azure portal.</span></span>

2. <span data-ttu-id="03249-170">Selecione uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="03249-170">Select a storage account.</span></span>

3. <span data-ttu-id="03249-171">Em configurações, na seção de serviço Blob hello, selecione a criptografia.</span><span class="sxs-lookup"><span data-stu-id="03249-171">In Settings, under hello Blob Service section, select Encryption.</span></span>

4. <span data-ttu-id="03249-172">Em Olá seção serviço do arquivo, selecione a criptografia.</span><span class="sxs-lookup"><span data-stu-id="03249-172">Under hello File Service section, select Encryption.</span></span>

<span data-ttu-id="03249-173">Depois de clicar em configuração de criptografia hello, você pode habilitar ou desabilitar a criptografia do serviço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="03249-173">After you click hello Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

<span data-ttu-id="03249-174">Novos dados serão criptografados.</span><span class="sxs-lookup"><span data-stu-id="03249-174">New data will be encrypted.</span></span> <span data-ttu-id="03249-175">Os dados em arquivos existentes nesta conta de armazenamento permanecerão não criptografados.</span><span class="sxs-lookup"><span data-stu-id="03249-175">Data in existing files in this storage account will remain unencrypted.</span></span>

<span data-ttu-id="03249-176">Depois de habilitar a criptografia, copie a conta de armazenamento toohello dados usando um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="03249-176">After enabling encryption, copy data toohello storage account using one of hello following methods:</span></span>

1. <span data-ttu-id="03249-177">Copiar blobs ou arquivos com hello [utilitário de linha de comando AzCopy](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span><span class="sxs-lookup"><span data-stu-id="03249-177">Copy blobs or files with hello [AzCopy Command Line utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span></span>

2. <span data-ttu-id="03249-178">[Montar um compartilhamento de arquivos usando SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) , você pode usar um utilitário como o Robocopy toocopy arquivos.</span><span class="sxs-lookup"><span data-stu-id="03249-178">[Mount a file share using SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) so you can use a utility such as Robocopy toocopy files.</span></span>

3. <span data-ttu-id="03249-179">Copiar blob ou arquivo de dados tooand do armazenamento de blob ou entre contas de armazenamento usando [bibliotecas de cliente de armazenamento como .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span><span class="sxs-lookup"><span data-stu-id="03249-179">Copy blob or file data tooand from blob storage or between storage accounts using [Storage Client Libraries such as .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

4.  <span data-ttu-id="03249-180">Use um [Gerenciador de armazenamento](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload tooyour conta de armazenamento de blobs com criptografia ativada.</span><span class="sxs-lookup"><span data-stu-id="03249-180">Use a [Storage Explorer](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload blobs tooyour storage account with encryption enabled.</span></span>

### <a name="transparent-data-encryption"></a><span data-ttu-id="03249-181">Transparent Data Encryption</span><span class="sxs-lookup"><span data-stu-id="03249-181">Transparent Data Encryption</span></span>

<span data-ttu-id="03249-182">Criptografia de dados transparente (TDE) é um recurso do SQL Azure pelo qual você pode criptografar os dados em ambos os níveis de banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="03249-182">Transparent Data Encryption (TDE) is a feature in SQL Azure by which you can encrypt data at both hello database and server levels.</span></span> <span data-ttu-id="03249-183">A TDE agora é habilitada por padrão em todos os bancos de dados recém-criados.</span><span class="sxs-lookup"><span data-stu-id="03249-183">TDE is now enabled by default on all newly created databases.</span></span> <span data-ttu-id="03249-184">A TDE realiza a criptografia de e/s e a descriptografia da saudação dados e arquivos de log em tempo real.</span><span class="sxs-lookup"><span data-stu-id="03249-184">TDE performs real-time I/O encryption and decryption of hello data and log files.</span></span>

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a><span data-ttu-id="03249-185">Como usa os dados pessoais do TDE tooprotect?</span><span class="sxs-lookup"><span data-stu-id="03249-185">How do I use TDE tooprotect personal data?</span></span>

<span data-ttu-id="03249-186">Você pode configurar TDE por meio de saudação portal do Azure, usando Olá API REST ou usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="03249-186">You can configure TDE through hello Azure portal, by using hello REST API, or by using PowerShell.</span></span> <span data-ttu-id="03249-187">tooenable TDE em um banco de dados existente usando Olá Portal do Azure, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="03249-187">tooenable TDE on an existing database using hello Azure Portal, do hello following:</span></span>

1. <span data-ttu-id="03249-188">Visite hello Azure portal em <https://portal.azure.com> e entrar com sua conta de administrador do Azure ou colaborador.</span><span class="sxs-lookup"><span data-stu-id="03249-188">Visit hello Azure portal at <https://portal.azure.com> and sign-in with your Azure Administrator or Contributor account.</span></span>

2. <span data-ttu-id="03249-189">Na faixa esquerda do hello, clique tooBROWSE e, em seguida, clique em bancos de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="03249-189">On hello left banner, click tooBROWSE, and then click SQL databases.</span></span>

3. <span data-ttu-id="03249-190">Com bancos de dados SQL selecionados no painel esquerdo do hello, clique em seu banco de dados do usuário.</span><span class="sxs-lookup"><span data-stu-id="03249-190">With SQL databases selected in hello left pane, click your user database.</span></span>

4. <span data-ttu-id="03249-191">Na folha de banco de dados de saudação, clique em todas as configurações.</span><span class="sxs-lookup"><span data-stu-id="03249-191">In hello database blade, click All settings.</span></span>

5. <span data-ttu-id="03249-192">Na folha de configurações de saudação, clique em folha de criptografia transparente de dados criptografia parte tooopen Olá transparente de dados.</span><span class="sxs-lookup"><span data-stu-id="03249-192">In hello Settings blade, click Transparent data encryption part tooopen hello Transparent data encryption blade.</span></span>

6. <span data-ttu-id="03249-193">Na folha de criptografia de dados hello, mover Olá tooOn de botão de criptografia de dados e, em seguida, clique em Salvar (na parte superior de saudação da página Olá) tooapply configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="03249-193">In hello Data encryption blade, move hello Data encryption button tooOn, and then click Save (at hello top of hello page) tooapply hello setting.</span></span> <span data-ttu-id="03249-194">Olá status de criptografia aproximará o progresso de Olá Olá transparente de criptografia de dados.</span><span class="sxs-lookup"><span data-stu-id="03249-194">hello Encryption status will approximate hello progress of hello transparent data encryption.</span></span>

![Habilitando a criptografia de dados](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

<span data-ttu-id="03249-196">Instruções sobre como o tooenable TDE e obter informações sobre a descriptografia de bancos de dados protegido por TDE e muito mais podem ser encontrados no artigo Olá [Transparent Data Encryption com o banco de dados do SQL Azure.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span><span class="sxs-lookup"><span data-stu-id="03249-196">Instructions on how tooenable TDE and information on decrypting TDE-protected databases and more can be found in hello article [Transparent Data Encryption with Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span></span>

## <a name="summary"></a><span data-ttu-id="03249-197">Resumo</span><span class="sxs-lookup"><span data-stu-id="03249-197">Summary</span></span>

<span data-ttu-id="03249-198">empresa Olá pode realizar sua meta de criptografar os dados pessoais armazenados na nuvem do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="03249-198">hello company can accomplish its goal of encrypting personal data stored in hello Azure cloud.</span></span> <span data-ttu-id="03249-199">Eles podem fazer isso usando a criptografia de disco do Azure muito proteger volumes inteiros.</span><span class="sxs-lookup"><span data-stu-id="03249-199">They can do this by using Azure Disk Encryption too protect entire volumes.</span></span> <span data-ttu-id="03249-200">Isso pode incluir arquivos do sistema operacional hello e arquivos de dados que contêm informações de identificação pessoal e outros dados confidenciais.</span><span class="sxs-lookup"><span data-stu-id="03249-200">This may include both hello operating system files and data files that hold personal identifiable information and other sensitive data.</span></span> <span data-ttu-id="03249-201">Criptografia do serviço de armazenamento do Azure pode ser usado tooprotect dados pessoais que são armazenados em arquivos e blobs.</span><span class="sxs-lookup"><span data-stu-id="03249-201">Azure Storage Service encryption can be used tooprotect personal data that is stored in blobs and files.</span></span> <span data-ttu-id="03249-202">Para dados armazenados em bancos de dados SQL do Azure, a Transparent Data Encryption oferece proteção contra a exposição não autorizada de informações pessoais.</span><span class="sxs-lookup"><span data-stu-id="03249-202">For data that is stored in Azure SQL databases, Transparent Data Encryption provides protection from unauthorized exposure of personal information.</span></span>

<span data-ttu-id="03249-203">tooprotect Olá as chaves usadas tooencrypt dados no Azure, a empresa de Olá pode usar o Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="03249-203">tooprotect hello keys that are used tooencrypt data in Azure, hello company can use Azure Key Vault.</span></span> <span data-ttu-id="03249-204">Isso simplifica o processo de gerenciamento de chaves de saudação e habilita Olá controle toomaintain de empresa de chaves que acessam e criptografar dados pessoais.</span><span class="sxs-lookup"><span data-stu-id="03249-204">This streamlines hello key management process and enables hello company toomaintain control of keys that access and encrypt personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03249-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="03249-205">Next steps</span></span>

- [<span data-ttu-id="03249-206">Guia de solução de problemas do Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="03249-206">Azure Disk Encryption Troubleshooting Guide</span></span>](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [<span data-ttu-id="03249-207">Criptografar uma Máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="03249-207">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [<span data-ttu-id="03249-208">Criptografia de dados no Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="03249-208">Encryption of data in Azure Data Lake Store</span></span>](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [<span data-ttu-id="03249-209">Criptografia de banco de dados em repouso do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="03249-209">Azure Cosmos DB database encryption at rest</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
