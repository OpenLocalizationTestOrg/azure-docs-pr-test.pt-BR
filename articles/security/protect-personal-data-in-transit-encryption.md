---
title: "dados pessoais aaaProtect em trânsito com criptografia no Azure | Microsoft Docs"
description: Usando a criptografia em dados pessoais tooprotect do Azure
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
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a><span data-ttu-id="9fc3a-103">Tecnologias de criptografia do Azure: proteger dados pessoais em trânsito com criptografia</span><span class="sxs-lookup"><span data-stu-id="9fc3a-103">Azure encryption technologies: Protect personal data in transit with encryption</span></span>

<span data-ttu-id="9fc3a-104">Este artigo o ajudará a entender e usar dados de toosecure de tecnologias de criptografia do Azure em trânsito.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-104">This article will help you understand and use Azure encryption technologies toosecure data in transit.</span></span> 

<span data-ttu-id="9fc3a-105">Privacidade de saudação proteção dos dados pessoais enquanto trafegam pela rede Olá é uma parte essencial de uma estratégia de segurança em várias camadas de defesa em profundidade.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-105">Protecting hello privacy of personal data as it travels across hello network is an essential part of a multi-layered defense-in-depth security strategy.</span></span> <span data-ttu-id="9fc3a-106">A criptografia em trânsito é projetado tooprevent um invasor intercepta as transmissões de ser capaz de dados de saudação tooview ou usar.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-106">Encryption in transit is designed tooprevent an attacker who intercepts transmissions from being able tooview or use hello data.</span></span>

## <a name="scenario"></a><span data-ttu-id="9fc3a-107">Cenário</span><span class="sxs-lookup"><span data-stu-id="9fc3a-107">Scenario</span></span>

<span data-ttu-id="9fc3a-108">Uma empresa cruzeiro grandes, com sede Olá dos Estados Unidos, está expandindo suas roteiros de toooffer operações Mediterrâneo hello, Adriatic e mares báltico, bem como Olá Britânicas.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="9fc3a-109">toosupport os esforços adquiriu várias linhas de cruzeiro menores na Itália, Alemanha, Dinamarca e hello UK</span><span class="sxs-lookup"><span data-stu-id="9fc3a-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="9fc3a-110">empresa de saudação usa dados corporativos do Microsoft Azure toostore na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="9fc3a-111">Eles incluem informações de identificação pessoal, como nomes, endereços, números de telefone e informações de cartão de crédito de sua base global de clientes.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-111">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="9fc3a-112">Ele também inclui informações de recursos humanos tradicionais, como endereços, números de telefone, números de identificação de imposto e médicas informações sobre os funcionários da empresa em todos os locais.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-112">It also includes traditional Human Resource information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="9fc3a-113">linha de cruzeiro Olá também mantém um banco de dados grande de membros do programa de recompensa e fidelidade que incluem informações pessoais tootrack relações com os clientes atuais e anteriores.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-113">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="9fc3a-114">Dados pessoais de clientes são inseridos no banco de dados de saudação de escritórios remotos da empresa Olá em agentes Olá mundo todo.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-114">Personal data of customers is entered in hello database from hello company’s remote offices and from travel agents located around hello world.</span></span> <span data-ttu-id="9fc3a-115">Documentos que contêm informações de cliente são transferidos entre Olá rede tooAzure de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-115">Documents containing customer information are transferred across hello network tooAzure storage.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="9fc3a-116">Problema declarado</span><span class="sxs-lookup"><span data-stu-id="9fc3a-116">Problem statement</span></span>

<span data-ttu-id="9fc3a-117">empresa Olá deve proteger a privacidade de saudação do cliente e dados pessoais de funcionários enquanto ele estão em trânsito tooand dos serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-117">hello company must protect hello privacy of customers’ and employees’ personal data while it is in transit tooand from Azure services.</span></span>

## <a name="company-goal"></a><span data-ttu-id="9fc3a-118">Meta da empresa</span><span class="sxs-lookup"><span data-stu-id="9fc3a-118">Company goal</span></span>

<span data-ttu-id="9fc3a-119">Olá tooensure de meta da empresa que dados pessoais são criptografados quando desativar o disco.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-119">hello company goal tooensure that personal data is encrypted when off disk.</span></span> <span data-ttu-id="9fc3a-120">Se pessoas não autorizadas interceptarem dados pessoais do hello fora do disco, ele deve ser em um formulário que será renderizado ilegível.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-120">If unauthorized persons intercept hello off-disk personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="9fc3a-121">A aplicação da criptografia deve ser fácil ou completamente transparente, para os usuários e administradores.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-121">Applying encryption should be easy, or completely transparent, for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="9fc3a-122">Soluções</span><span class="sxs-lookup"><span data-stu-id="9fc3a-122">Solutions</span></span>

<span data-ttu-id="9fc3a-123">Os serviços do Azure fornecem vários toohelp ferramentas e tecnologias de proteger dados pessoais em trânsito.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-123">Azure services provide multiple tools and technologies toohelp you protect personal data in transit.</span></span>

### <a name="azure-storage"></a><span data-ttu-id="9fc3a-124">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="9fc3a-124">Azure Storage</span></span>

<span data-ttu-id="9fc3a-125">Dados armazenados na nuvem Olá devem passar de cliente hello, que pode estar fisicamente localizado em qualquer lugar no mundo hello, toohello data center do Azure.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-125">Data that is stored in hello cloud must travel from hello client, which can be physically located anywhere in hello world, toohello Azure data center.</span></span> <span data-ttu-id="9fc3a-126">Quando os dados são recuperados por usuários, novamente, trafegam na Olá oposta direção.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-126">When that data is retrieved by users, it travels again, in hello opposite direction.</span></span> <span data-ttu-id="9fc3a-127">Dados que estão em trânsito Olá Internet pública sempre está em risco de interceptação por invasores.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-127">Data that is in transit over hello public Internet is always at risk of interception by attackers.</span></span> <span data-ttu-id="9fc3a-128">É importante tooprotect privacidade de saudação dos dados pessoais usando criptografia de nível de transporte toosecure como ele se move entre locais.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-128">It is important tooprotect hello privacy of personal data by using transport-level encryption toosecure it as it moves between locations.</span></span>

<span data-ttu-id="9fc3a-129">Olá protocolo HTTPS fornece um canal de comunicação seguro e criptografado em relação a saudação da Internet.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-129">hello HTTPS protocol provides a secure, encrypted communications channel over hello Internet.</span></span> <span data-ttu-id="9fc3a-130">HTTPS deve ser usado tooaccess objetos no armazenamento do Azure e ao chamar APIs REST.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-130">HTTPS should be used tooaccess objects in Azure Storage and when calling REST APIs.</span></span> <span data-ttu-id="9fc3a-131">Impor o uso do protocolo HTTPS Olá ao usar [assinaturas de acesso compartilhado](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) objetos de armazenamento (SAS) toodelegate acesso tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-131">You enforce use of hello HTTPS protocol when using [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate access tooAzure Storage objects.</span></span> <span data-ttu-id="9fc3a-132">Há dois tipos de SAS: SAS de Serviço e SAS de Conta.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-132">There are two types of SAS: Service SAS and Account SAS.</span></span>

#### <a name="how-do-i-construct-a-service-sas"></a><span data-ttu-id="9fc3a-133">Como fazer para construir uma SAS de Serviço?</span><span class="sxs-lookup"><span data-stu-id="9fc3a-133">How do I construct a Service SAS?</span></span>

<span data-ttu-id="9fc3a-134">Um serviço SAS delegados acesso tooa recurso em apenas um dos serviços de armazenamento da saudação (serviço blob, fila, tabela ou arquivo).</span><span class="sxs-lookup"><span data-stu-id="9fc3a-134">A Service SAS delegates access tooa resource in just one of hello storage services (blob, queue, table or file service).</span></span> <span data-ttu-id="9fc3a-135">tooconstruct uma SAS do serviço, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="9fc3a-135">tooconstruct a Service SAS, do hello following:</span></span>

1. <span data-ttu-id="9fc3a-136">Especifique a saudação o campo de versão assinado</span><span class="sxs-lookup"><span data-stu-id="9fc3a-136">Specify hello Signed Version Field</span></span>

2. <span data-ttu-id="9fc3a-137">Especifique a saudação recurso assinado (Blob e somente serviço de arquivo)</span><span class="sxs-lookup"><span data-stu-id="9fc3a-137">Specify hello Signed Resource (Blob and File Service Only)</span></span>

3. <span data-ttu-id="9fc3a-138">Especificar parâmetros de consulta tooOverride cabeçalhos de resposta (serviço Blob e arquivo de serviço somente)</span><span class="sxs-lookup"><span data-stu-id="9fc3a-138">Specify Query Parameters tooOverride Response Headers (Blob Service and File Service Only)</span></span>

4. <span data-ttu-id="9fc3a-139">Especifique a saudação nome da tabela (serviço de tabela somente)</span><span class="sxs-lookup"><span data-stu-id="9fc3a-139">Specify hello Table Name (Table Service Only)</span></span>

5. <span data-ttu-id="9fc3a-140">Especifique a política de acesso de saudação</span><span class="sxs-lookup"><span data-stu-id="9fc3a-140">Specify hello Access Policy</span></span>

6. <span data-ttu-id="9fc3a-141">Especifique a saudação intervalo de validade da assinatura</span><span class="sxs-lookup"><span data-stu-id="9fc3a-141">Specify hello Signature Validity Interval</span></span>

8. <span data-ttu-id="9fc3a-142">Especifique as permissões</span><span class="sxs-lookup"><span data-stu-id="9fc3a-142">Specify Permissions</span></span>

9. <span data-ttu-id="9fc3a-143">Especifique o endereço IP ou o intervalo de IP</span><span class="sxs-lookup"><span data-stu-id="9fc3a-143">Specify IP Address or IP Range</span></span>

10. <span data-ttu-id="9fc3a-144">Especifique a saudação protocolo HTTP</span><span class="sxs-lookup"><span data-stu-id="9fc3a-144">Specify hello HTTP Protocol</span></span>

11. <span data-ttu-id="9fc3a-145">Especifique os intervalos de acesso da tabela</span><span class="sxs-lookup"><span data-stu-id="9fc3a-145">Specify Table Access Ranges</span></span>

12. <span data-ttu-id="9fc3a-146">Especifique a saudação identificador assinado</span><span class="sxs-lookup"><span data-stu-id="9fc3a-146">Specify hello Signed Identifier</span></span>

13. <span data-ttu-id="9fc3a-147">Especifique a saudação assinatura</span><span class="sxs-lookup"><span data-stu-id="9fc3a-147">Specify hello Signature</span></span>

<span data-ttu-id="9fc3a-148">Para obter instruções mais detalhadas, consulte [Construindo uma SAS de Serviço](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="9fc3a-148">For more detailed instructions, see [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span></span>

#### <a name="how-do-i-construct-an-account-sas"></a><span data-ttu-id="9fc3a-149">Como fazer para construir uma SAS de Conta?</span><span class="sxs-lookup"><span data-stu-id="9fc3a-149">How do I construct an Account SAS?</span></span>

<span data-ttu-id="9fc3a-150">Uma SAS da conta delega tooresources de acesso em um ou mais dos serviços de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-150">An Account SAS delegates access tooresources in one or more of hello storage services.</span></span> <span data-ttu-id="9fc3a-151">Você também pode delegar acesso tooread, gravação e operações de exclusão em contêineres de blob, tabelas, filas e compartilhamentos de arquivos que não são permitidos com um serviço de SAS.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-151">You can also delegate access tooread, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="9fc3a-152">Construção de uma conta de SAS é semelhante toothat de uma SAS do serviço.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-152">Construction of an Account SAS is similar toothat of a Service SAS.</span></span> <span data-ttu-id="9fc3a-153">Para obter instruções detalhadas, consulte [Construindo uma SAS de Conta.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="9fc3a-153">For detailed instructions, see [Constructing an Account SAS.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span></span>

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a><span data-ttu-id="9fc3a-154">Como fazer para impor o HTTPS ao chamar APIs REST?</span><span class="sxs-lookup"><span data-stu-id="9fc3a-154">How do I enforce HTTPS when calling REST APIs?</span></span>

<span data-ttu-id="9fc3a-155">tooenforce o uso de saudação de HTTPS ao chamar objetos tooaccess de APIs REST em contas de armazenamento, você pode habilitar Secure transferir necessário Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-155">tooenforce hello use of HTTPS when calling REST APIs tooaccess objects in storage accounts, you can enable Secure Transfer Required for hello storage account.</span></span> 

1. <span data-ttu-id="9fc3a-156">No portal do Azure de Olá, selecione **criar conta de armazenamento**, ou para uma conta de armazenamento existente, selecione **configurações** e, em seguida, **configuração**.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-156">In hello Azure portal, select **Create Storage Account**, or for an existing storage account, select **Settings** and then **Configuration**.</span></span>

2. <span data-ttu-id="9fc3a-157">Em **Transferência Segura Obrigatória**, selecione **Habilitada**.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-157">Under **Secure Transfer Required**, select **Enabled**.</span></span>

![Criando uma conta de armazenamento](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

<span data-ttu-id="9fc3a-159">Para obter instruções mais detalhadas, incluindo como tooenable proteger transferir obrigatório programaticamente, consulte [precisam proteger transferir](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span><span class="sxs-lookup"><span data-stu-id="9fc3a-159">For more detailed instructions, including how tooenable Secure Transfer Required programmatically, see [Require Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span></span>

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a><span data-ttu-id="9fc3a-160">Como fazer para criptografar dados no Armazenamento de Arquivos do Azure?</span><span class="sxs-lookup"><span data-stu-id="9fc3a-160">How do I encrypt data in Azure File Storage?</span></span>

<span data-ttu-id="9fc3a-161">tooencrypt dados em trânsito com [armazenamento de arquivo do Azure](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), você pode usar o SMB 3. x com o Windows 8, 8.1 e 10 e Windows Server 2012 R2 e Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-161">tooencrypt data in transit with [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), you can use SMB 3.x with Windows 8, 8.1, and 10 and with Windows Server 2012 R2 and Windows Server 2016.</span></span> <span data-ttu-id="9fc3a-162">Quando você estiver usando o serviço de arquivos do Azure Olá, qualquer conexão sem criptografia falhará ao "Seguro transferência necessária" está habilitado.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-162">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="9fc3a-163">Isso inclui cenários de uso de SMB 2.1, SMB 3.0 sem criptografia e alguns tipos de saudação cliente Linux SMB.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-163">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span>

#### <a name="azure-client-side-encryption"></a><span data-ttu-id="9fc3a-164">Criptografia do Lado do Cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="9fc3a-164">Azure Client-Side Encryption</span></span>

<span data-ttu-id="9fc3a-165">Outra opção para proteger dados pessoais enquanto estão sendo transferidos entre um aplicativo cliente e o Armazenamento do Azure é a [Criptografia do Lado do Cliente](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span><span class="sxs-lookup"><span data-stu-id="9fc3a-165">Another option for protecting personal data while it’s being transferred between a client application and Azure Storage is [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span></span> <span data-ttu-id="9fc3a-166">Olá dados são criptografados antes de serem transferidos para o armazenamento do Azure e ao recuperar dados de saudação do armazenamento do Azure, os dados de saudação são descriptografados depois de ser recebida no lado do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-166">hello data is encrypted before being transferred into Azure Storage and when you retrieve hello data from Azure Storage, hello data is decrypted after it is received on hello client side.</span></span>

### <a name="azure-site-to-site-vpn"></a><span data-ttu-id="9fc3a-167">VPN site a site do Azure</span><span class="sxs-lookup"><span data-stu-id="9fc3a-167">Azure Site-to-Site VPN</span></span>

<span data-ttu-id="9fc3a-168">Um maneira eficiente tooprotect pessoal os dados em trânsito entre uma rede corporativa ou o usuário e a saudação rede virtual do Azure são toouse uma [site a site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) ou [ponto a site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) rede Virtual privada (VPN).</span><span class="sxs-lookup"><span data-stu-id="9fc3a-168">An effective way tooprotect personal data in transit between a corporate network or user and hello Azure virtual network is toouse a [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) or [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) Virtual Private Network (VPN).</span></span> <span data-ttu-id="9fc3a-169">Uma conexão VPN cria um encapsulamento criptografado seguro em Olá da Internet.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-169">A VPN connection creates a secure encrypted tunnel across hello Internet.</span></span>

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a><span data-ttu-id="9fc3a-170">Como fazer para criar uma conexão VPN site a site?</span><span class="sxs-lookup"><span data-stu-id="9fc3a-170">How do I create a site-to-site VPN connection?</span></span>

<span data-ttu-id="9fc3a-171">Uma VPN site a site se conecta a vários usuários em Olá tooAzure de rede corporativa.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-171">A site-to-site VPN connects multiple users on hello corporate network tooAzure.</span></span> <span data-ttu-id="9fc3a-172">toocreate uma conexão site a site no hello portal do Azure, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="9fc3a-172">toocreate a site-to-site connection in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="9fc3a-173">Crie uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-173">Create a virtual network.</span></span>

2. <span data-ttu-id="9fc3a-174">Especifique um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-174">Specify a DNS server.</span></span>

3. <span data-ttu-id="9fc3a-175">Crie uma sub-rede de gateway hello.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-175">Create hello gateway subnet.</span></span>

4. <span data-ttu-id="9fc3a-176">Crie gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-176">Create hello VPN gateway.</span></span> 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. <span data-ttu-id="9fc3a-177">Crie gateway de rede local hello.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-177">Create hello local network gateway.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. <span data-ttu-id="9fc3a-178">Configure o dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-178">Configure your VPN device.</span></span>

7. <span data-ttu-id="9fc3a-179">Crie conexão de VPN hello.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-179">Create hello VPN connection.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. <span data-ttu-id="9fc3a-180">Verifique se a conexão de VPN hello.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-180">Verify hello VPN connection.</span></span>

<span data-ttu-id="9fc3a-181">Para obter instruções mais detalhadas sobre como conexão toocreate uma site a site no hello Azure portal, consulte [criar uma Site a Site conexão no hello Portal do Azure]. (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="9fc3a-181">For more detailed instructions on how toocreate a site-to-site connection in hello Azure portal, see [Create a Site-to-Site  connection in hello Azure Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span></span>

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a><span data-ttu-id="9fc3a-182">Como fazer para criar uma conexão VPN ponto a site?</span><span class="sxs-lookup"><span data-stu-id="9fc3a-182">How do I create a point-to-site VPN connection?</span></span>

<span data-ttu-id="9fc3a-183">Uma VPN ponto a Site cria uma conexão segura de uma rede virtual do computador tooa de clientes individuais.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-183">A Point-to-Site VPN creates a secure connection from an individual client computer tooa virtual network.</span></span> <span data-ttu-id="9fc3a-184">Isso é útil quando você deseja tooAzure tooconnect de um local remoto, como de central casa ou em um hotel ou conferência.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-184">This is useful when you  want tooconnect tooAzure from a remote location, such as from home or a hotel or conference center.</span></span> <span data-ttu-id="9fc3a-185">toocreate uma conexão ponto a site no hello portal do Azure,</span><span class="sxs-lookup"><span data-stu-id="9fc3a-185">toocreate a point-to-site  connection in hello Azure portal,</span></span>

1. <span data-ttu-id="9fc3a-186">Crie uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-186">Create a virtual network.</span></span>

2. <span data-ttu-id="9fc3a-187">Adicione uma sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-187">Add a gateway subnet.</span></span>

3. <span data-ttu-id="9fc3a-188">Especifique um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-188">Specify a DNS server.</span></span> <span data-ttu-id="9fc3a-189">(opcional)</span><span class="sxs-lookup"><span data-stu-id="9fc3a-189">(optional)</span></span>

4. <span data-ttu-id="9fc3a-190">Crie um gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-190">Create a virtual network gateway.</span></span>

5. <span data-ttu-id="9fc3a-191">Gere certificados.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-191">Generate certificates.</span></span>

6. <span data-ttu-id="9fc3a-192">Adicione pool de endereços de cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-192">Add hello client address pool.</span></span>

7. <span data-ttu-id="9fc3a-193">Carregar dados de certificado pública do certificado de raiz hello.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-193">Upload hello root certificate public certificate data.</span></span>

8. <span data-ttu-id="9fc3a-194">Gerar e instale o pacote de configuração de cliente VPN hello.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-194">Generate and install hello VPN client configuration package.</span></span>

9. <span data-ttu-id="9fc3a-195">Instale um certificado do cliente exportado.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-195">Install an exported client certificate.</span></span>

10. <span data-ttu-id="9fc3a-196">Conecte-se tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-196">Connect tooAzure.</span></span>

11. <span data-ttu-id="9fc3a-197">Verifique a conexão.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-197">Verify your connection.</span></span>

<span data-ttu-id="9fc3a-198">Para obter instruções mais detalhadas, consulte [configurar uma conexão de ponto para Site tooa VNet usando a autenticação de certificado: Portal do Azure.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="9fc3a-198">For more detailed instructions, see [Configure a Point-to-Site connection tooa VNet using certificate authentication: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span></span>

### <a name="ssltls"></a><span data-ttu-id="9fc3a-199">SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="9fc3a-199">SSL/TLS</span></span>

<span data-ttu-id="9fc3a-200">A Microsoft recomenda que você sempre use dados de tooexchange protocolos SSL/TLS em diferentes locais.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-200">Microsoft recommends that you always use SSL/TLS protocols tooexchange data across different locations.</span></span> <span data-ttu-id="9fc3a-201">As organizações que escolha toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove grandes conjuntos de dados em um link WAN de alta velocidade dedicado também pode criptografar dados Olá Olá usando SSL/TLS ou outros protocolos para proteção adicional de nível de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-201">Organizations that choose toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove large data sets over a dedicated high-speed WAN link can also encrypt hello data at hello application-level using SSL/TLS or other protocols for added protection.</span></span>

### <a name="encryption-by-default"></a><span data-ttu-id="9fc3a-202">Criptografia por padrão</span><span class="sxs-lookup"><span data-stu-id="9fc3a-202">Encryption by default</span></span>

<span data-ttu-id="9fc3a-203">A Microsoft usa os dados de tooprotect de criptografia em trânsito entre clientes e serviços de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-203">Microsoft uses encryption tooprotect data in transit between customers and Azure cloud services.</span></span> <span data-ttu-id="9fc3a-204">Se você estiver interagindo com o armazenamento do Azure por meio de saudação Portal do Azure, todas as transações ocorrem por meio de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-204">If you are interacting with Azure Storage through hello Azure Portal, all transactions occur via HTTPS.</span></span>

<span data-ttu-id="9fc3a-205">[Segurança de camada de transporte](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) é o protocolo de saudação que data centers da Microsoft tentará toonegotiate com sistemas de cliente que se conectam tooMicrosoft serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is hello protocol that Microsoft data centers will attempt toonegotiate with client systems that connect tooMicrosoft cloud services.</span></span> <span data-ttu-id="9fc3a-206">O TLS fornece autenticação forte, privacidade de mensagem e integridade (habilita a detecção de adulteração, interceptação e falsificação de mensagens), interoperabilidade, flexibilidade de algoritmo, facilidade de implantação e uso.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-206">TLS provides strong authentication, message privacy, and integrity (enables detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, ease of deployment and use.</span></span>

<span data-ttu-id="9fc3a-207">O [PFS](https://en.wikipedia.org/wiki/Forward_secrecy) (Perfect Forward Secrecy) também é utilizado para que cada conexão entre os sistemas cliente dos clientes e os serviços de nuvem da Microsoft usem chaves exclusivas.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is also employed so that each connection between customers’ client systems and Microsoft’s cloud services use unique keys.</span></span> <span data-ttu-id="9fc3a-208">Serviços de nuvem tooMicrosoft conexões também tirar proveito de criptografia de 2.048 bits RSA com comprimentos de chave.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-208">Connections tooMicrosoft cloud services also take advantage of RSA based 2,048-bit encryption key lengths.</span></span> <span data-ttu-id="9fc3a-209">Olá combinação de TLS, comprimentos de chave RSA de 2.048 bits, e PFS torna muito mais difícil para alguém toointercept e acessar dados em trânsito entre clientes e serviços de nuvem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-209">hello combination of TLS, RSA 2,048-bit key lengths, and PFS makes it much  more difficult for someone toointercept and access data that is in transit between Microsoft cloud services and customers.</span></span>

<span data-ttu-id="9fc3a-210">Os dados em trânsito são Always Encrypted no [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span><span class="sxs-lookup"><span data-stu-id="9fc3a-210">Data in transit is always encrypted in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span></span> <span data-ttu-id="9fc3a-211">Além disso mídia toopersistent do tooencrypting dados toostoring anterior, Olá dados são sempre protegidos em trânsito usando HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-211">In addition tooencrypting data prior toostoring toopersistent media, hello data is also always secured in transit by using HTTPS.</span></span> <span data-ttu-id="9fc3a-212">HTTPS é Olá único protocolo com suporte para Olá que interfaces Data Lake repositório REST.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-212">HTTPS is hello only protocol that is supported for hello Data Lake Store REST interfaces.</span></span>

## <a name="summary"></a><span data-ttu-id="9fc3a-213">Resumo</span><span class="sxs-lookup"><span data-stu-id="9fc3a-213">Summary</span></span>

<span data-ttu-id="9fc3a-214">empresa Olá pode fazer o seu objetivo de proteção de privacidade de dados e hello pessoal desses dados impondo HTTPS conexões tooAzure armazenamento, usando assinaturas de acesso compartilhado e habilitando seguro transferir necessárias em contas de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-214">hello company can accomplish its goal of protecting personal data and hello privacy of such data by enforcing HTTPS connections tooAzure Storage, using Shared Access Signatures and enabling Secure Transfer Required on hello storage accounts.</span></span> <span data-ttu-id="9fc3a-215">Ela também pode proteger os dados pessoais usando conexões SMB 3.0 e implementando a criptografia do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-215">They can also protect personal data by using SMB 3.0 connections and implementing client-side encryption.</span></span> <span data-ttu-id="9fc3a-216">Olá de conexões de VPN site a site da rede corporativa toohello rede virtual do Azure e conexões de VPN de ponto para site de usuários individuais criará um túnel seguro por meio do qual dados pessoais podem viajar com segurança.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-216">Site-to-site VPN connections from hello corporate network toohello Azure virtual network and point-to-site VPN connections from individual users will create a secure tunnel through which personal data can securely travel.</span></span> <span data-ttu-id="9fc3a-217">Práticas recomendadas de criptografia de padrão da Microsoft serão proteger ainda mais privacidade Olá dos dados pessoais.</span><span class="sxs-lookup"><span data-stu-id="9fc3a-217">Microsoft’s default encryption practices will further protect hello privacy of personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fc3a-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9fc3a-218">Next steps</span></span>

- [<span data-ttu-id="9fc3a-219">Melhores práticas de segurança de dados e criptografia do Azure</span><span class="sxs-lookup"><span data-stu-id="9fc3a-219">Azure Data Security and Encryption Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [<span data-ttu-id="9fc3a-220">Planejamento e design do Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="9fc3a-220">Planning and design for VPN Gateway</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [<span data-ttu-id="9fc3a-221">Perguntas frequentes de gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="9fc3a-221">VPN Gateway FAQ</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [<span data-ttu-id="9fc3a-222">Comprar e configurar um certificado SSL para o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="9fc3a-222">Buy and configure an SSL Certificate for your Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
