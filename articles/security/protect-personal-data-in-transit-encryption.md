---
title: "Proteger dados pessoais em trânsito com a criptografia no Azure | Microsoft Docs"
description: Usando a criptografia no Azure para proteger dados pessoais
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
ms.openlocfilehash: 99e40b8a09a2f151e7f83fbb58bdfc00ae4b1268
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a><span data-ttu-id="f45b6-103">Tecnologias de criptografia do Azure: proteger dados pessoais em trânsito com criptografia</span><span class="sxs-lookup"><span data-stu-id="f45b6-103">Azure encryption technologies: Protect personal data in transit with encryption</span></span>

<span data-ttu-id="f45b6-104">Este artigo ajudará você a entender e usar as tecnologias de criptografia do Azure para proteger dados em trânsito.</span><span class="sxs-lookup"><span data-stu-id="f45b6-104">This article will help you understand and use Azure encryption technologies to secure data in transit.</span></span> 

<span data-ttu-id="f45b6-105">A proteção da privacidade de dados pessoais durante seu tráfego pela rede é uma parte essencial de uma estratégia de segurança de proteção avançada de várias camadas.</span><span class="sxs-lookup"><span data-stu-id="f45b6-105">Protecting the privacy of personal data as it travels across the network is an essential part of a multi-layered defense-in-depth security strategy.</span></span> <span data-ttu-id="f45b6-106">A criptografia em trânsito foi projetada para impedir que um invasor que intercepta as transmissões consiga exibir ou usar os dados.</span><span class="sxs-lookup"><span data-stu-id="f45b6-106">Encryption in transit is designed to prevent an attacker who intercepts transmissions from being able to view or use the data.</span></span>

## <a name="scenario"></a><span data-ttu-id="f45b6-107">Cenário</span><span class="sxs-lookup"><span data-stu-id="f45b6-107">Scenario</span></span>

<span data-ttu-id="f45b6-108">Uma empresa de cruzeiro de grande porte, com sede nos Estados Unidos, está expandindo suas operações para oferecer roteiros nos mares Mediterrâneo, Adriático e Báltico, bem como nas Ilhas Britânicas.</span><span class="sxs-lookup"><span data-stu-id="f45b6-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="f45b6-109">Para dar suporte a esses esforços, ela adquiriu várias linhas de cruzeiro menores localizadas na Itália, na Alemanha, na Dinamarca e no Reino Unido.</span><span class="sxs-lookup"><span data-stu-id="f45b6-109">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span> 

<span data-ttu-id="f45b6-110">A empresa usa o Microsoft Azure para armazenar dados corporativos na nuvem.</span><span class="sxs-lookup"><span data-stu-id="f45b6-110">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="f45b6-111">Eles incluem informações de identificação pessoal, como nomes, endereços, números de telefone e informações de cartão de crédito de sua base global de clientes.</span><span class="sxs-lookup"><span data-stu-id="f45b6-111">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="f45b6-112">Ele também inclui informações de recursos humanos tradicionais, como endereços, números de telefone, números de identificação de imposto e médicas informações sobre os funcionários da empresa em todos os locais.</span><span class="sxs-lookup"><span data-stu-id="f45b6-112">It also includes traditional Human Resource information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="f45b6-113">A linha de cruzeiro também mantém um banco de dados grande de membros do programa de recompensa e fidelidade que inclui informações pessoais para acompanhamento das relações com os clientes atuais e anteriores.</span><span class="sxs-lookup"><span data-stu-id="f45b6-113">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

<span data-ttu-id="f45b6-114">Os dados pessoais de clientes são inseridos no banco de dados em escritórios remotos da empresa e nos agentes de viagem localizados no mundo todo.</span><span class="sxs-lookup"><span data-stu-id="f45b6-114">Personal data of customers is entered in the database from the company’s remote offices and from travel agents located around the world.</span></span> <span data-ttu-id="f45b6-115">Os documentos que contêm informações de clientes são transferidos pela rede para o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f45b6-115">Documents containing customer information are transferred across the network to Azure storage.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="f45b6-116">Problema declarado</span><span class="sxs-lookup"><span data-stu-id="f45b6-116">Problem statement</span></span>

<span data-ttu-id="f45b6-117">A empresa deve proteger a privacidade dos dados pessoais de clientes e funcionários enquanto eles estão em trânsito entre os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="f45b6-117">The company must protect the privacy of customers’ and employees’ personal data while it is in transit to and from Azure services.</span></span>

## <a name="company-goal"></a><span data-ttu-id="f45b6-118">Meta da empresa</span><span class="sxs-lookup"><span data-stu-id="f45b6-118">Company goal</span></span>

<span data-ttu-id="f45b6-119">A meta da empresa é garantir que os dados pessoais sejam criptografados quando estiverem fora do disco.</span><span class="sxs-lookup"><span data-stu-id="f45b6-119">The company goal to ensure that personal data is encrypted when off disk.</span></span> <span data-ttu-id="f45b6-120">Caso pessoas não autorizadas interceptem dados pessoais fora do disco, eles devem estar em um formato que os tornará ilegíveis.</span><span class="sxs-lookup"><span data-stu-id="f45b6-120">If unauthorized persons intercept the off-disk personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="f45b6-121">A aplicação da criptografia deve ser fácil ou completamente transparente, para os usuários e administradores.</span><span class="sxs-lookup"><span data-stu-id="f45b6-121">Applying encryption should be easy, or completely transparent, for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="f45b6-122">Soluções</span><span class="sxs-lookup"><span data-stu-id="f45b6-122">Solutions</span></span>

<span data-ttu-id="f45b6-123">Os serviços do Azure fornecem várias ferramentas e tecnologias para ajudá-lo a proteger dados pessoais em trânsito.</span><span class="sxs-lookup"><span data-stu-id="f45b6-123">Azure services provide multiple tools and technologies to help you protect personal data in transit.</span></span>

### <a name="azure-storage"></a><span data-ttu-id="f45b6-124">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f45b6-124">Azure Storage</span></span>

<span data-ttu-id="f45b6-125">Os dados armazenados na nuvem devem viajar do cliente, que pode estar localizado fisicamente em qualquer lugar do mundo, para o data center do Azure.</span><span class="sxs-lookup"><span data-stu-id="f45b6-125">Data that is stored in the cloud must travel from the client, which can be physically located anywhere in the world, to the Azure data center.</span></span> <span data-ttu-id="f45b6-126">Quando os dados são recuperados pelos usuários, eles viajam novamente, na direção oposta.</span><span class="sxs-lookup"><span data-stu-id="f45b6-126">When that data is retrieved by users, it travels again, in the opposite direction.</span></span> <span data-ttu-id="f45b6-127">Os dados em trânsito pela Internet pública sempre correm o risco de interceptação por invasores.</span><span class="sxs-lookup"><span data-stu-id="f45b6-127">Data that is in transit over the public Internet is always at risk of interception by attackers.</span></span> <span data-ttu-id="f45b6-128">É importante proteger a privacidade de dados pessoais usando a criptografia no nível de transporte para protegê-los enquanto eles se movem entre as localizações.</span><span class="sxs-lookup"><span data-stu-id="f45b6-128">It is important to protect the privacy of personal data by using transport-level encryption to secure it as it moves between locations.</span></span>

<span data-ttu-id="f45b6-129">O protocolo HTTPS fornece um canal de comunicação seguro, criptografado pela Internet.</span><span class="sxs-lookup"><span data-stu-id="f45b6-129">The HTTPS protocol provides a secure, encrypted communications channel over the Internet.</span></span> <span data-ttu-id="f45b6-130">O HTTPS deve ser usado para acessar objetos no Armazenamento do Azure e ao chamar APIs REST.</span><span class="sxs-lookup"><span data-stu-id="f45b6-130">HTTPS should be used to access objects in Azure Storage and when calling REST APIs.</span></span> <span data-ttu-id="f45b6-131">Imponha o uso do protocolo HTTPS ao usar [SAS](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (Assinaturas de Acesso Compartilhado) para delegar o acesso aos objetos do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f45b6-131">You enforce use of the HTTPS protocol when using [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) to delegate access to Azure Storage objects.</span></span> <span data-ttu-id="f45b6-132">Há dois tipos de SAS: SAS de Serviço e SAS de Conta.</span><span class="sxs-lookup"><span data-stu-id="f45b6-132">There are two types of SAS: Service SAS and Account SAS.</span></span>

#### <a name="how-do-i-construct-a-service-sas"></a><span data-ttu-id="f45b6-133">Como fazer para construir uma SAS de Serviço?</span><span class="sxs-lookup"><span data-stu-id="f45b6-133">How do I construct a Service SAS?</span></span>

<span data-ttu-id="f45b6-134">Uma SAS de serviço delega acesso a um recurso em apenas um dos serviços de armazenamento (serviço blob, fila, tabela ou arquivo).</span><span class="sxs-lookup"><span data-stu-id="f45b6-134">A Service SAS delegates access to a resource in just one of the storage services (blob, queue, table or file service).</span></span> <span data-ttu-id="f45b6-135">Para construir uma SAS de Serviço, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f45b6-135">To construct a Service SAS, do the following:</span></span>

1. <span data-ttu-id="f45b6-136">Especifique o campo de versão assinado</span><span class="sxs-lookup"><span data-stu-id="f45b6-136">Specify the Signed Version Field</span></span>

2. <span data-ttu-id="f45b6-137">Especifique o recurso assinado (somente serviço Blob e Arquivo)</span><span class="sxs-lookup"><span data-stu-id="f45b6-137">Specify the Signed Resource (Blob and File Service Only)</span></span>

3. <span data-ttu-id="f45b6-138">Especifique os parâmetros de consulta para substituir os cabeçalhos de resposta (somente serviço Blob e Arquivo)</span><span class="sxs-lookup"><span data-stu-id="f45b6-138">Specify Query Parameters to Override Response Headers (Blob Service and File Service Only)</span></span>

4. <span data-ttu-id="f45b6-139">Especifique o nome da tabela (somente serviço Tabela)</span><span class="sxs-lookup"><span data-stu-id="f45b6-139">Specify the Table Name (Table Service Only)</span></span>

5. <span data-ttu-id="f45b6-140">Especifique a política de acesso</span><span class="sxs-lookup"><span data-stu-id="f45b6-140">Specify the Access Policy</span></span>

6. <span data-ttu-id="f45b6-141">Especifique o intervalo de validade da assinatura</span><span class="sxs-lookup"><span data-stu-id="f45b6-141">Specify the Signature Validity Interval</span></span>

8. <span data-ttu-id="f45b6-142">Especifique as permissões</span><span class="sxs-lookup"><span data-stu-id="f45b6-142">Specify Permissions</span></span>

9. <span data-ttu-id="f45b6-143">Especifique o endereço IP ou o intervalo de IP</span><span class="sxs-lookup"><span data-stu-id="f45b6-143">Specify IP Address or IP Range</span></span>

10. <span data-ttu-id="f45b6-144">Especifique o protocolo HTTP</span><span class="sxs-lookup"><span data-stu-id="f45b6-144">Specify the HTTP Protocol</span></span>

11. <span data-ttu-id="f45b6-145">Especifique os intervalos de acesso da tabela</span><span class="sxs-lookup"><span data-stu-id="f45b6-145">Specify Table Access Ranges</span></span>

12. <span data-ttu-id="f45b6-146">Especifique o identificador assinado</span><span class="sxs-lookup"><span data-stu-id="f45b6-146">Specify the Signed Identifier</span></span>

13. <span data-ttu-id="f45b6-147">Especifique a assinatura</span><span class="sxs-lookup"><span data-stu-id="f45b6-147">Specify the Signature</span></span>

<span data-ttu-id="f45b6-148">Para obter instruções mais detalhadas, consulte [Construindo uma SAS de Serviço](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="f45b6-148">For more detailed instructions, see [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span></span>

#### <a name="how-do-i-construct-an-account-sas"></a><span data-ttu-id="f45b6-149">Como fazer para construir uma SAS de Conta?</span><span class="sxs-lookup"><span data-stu-id="f45b6-149">How do I construct an Account SAS?</span></span>

<span data-ttu-id="f45b6-150">Uma SAS de Conta delega acesso a recursos em um ou mais dos serviços de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f45b6-150">An Account SAS delegates access to resources in one or more of the storage services.</span></span> <span data-ttu-id="f45b6-151">Você também pode delegar acesso a operações de leitura, gravação e exclusão em contêineres de blob, tabelas, filas e compartilhamentos de arquivos que não são permitidos com um SAS de serviço.</span><span class="sxs-lookup"><span data-stu-id="f45b6-151">You can also delegate access to read, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="f45b6-152">A construção de uma SAS de Conta é semelhante a de uma SAS de Serviço.</span><span class="sxs-lookup"><span data-stu-id="f45b6-152">Construction of an Account SAS is similar to that of a Service SAS.</span></span> <span data-ttu-id="f45b6-153">Para obter instruções detalhadas, consulte [Construindo uma SAS de Conta.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="f45b6-153">For detailed instructions, see [Constructing an Account SAS.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span></span>

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a><span data-ttu-id="f45b6-154">Como fazer para impor o HTTPS ao chamar APIs REST?</span><span class="sxs-lookup"><span data-stu-id="f45b6-154">How do I enforce HTTPS when calling REST APIs?</span></span>

<span data-ttu-id="f45b6-155">Para impor o uso do HTTPS ao chamar APIs REST para acessar objetos em contas de armazenamento, habilite o recurso Transferência Segura Obrigatória na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f45b6-155">To enforce the use of HTTPS when calling REST APIs to access objects in storage accounts, you can enable Secure Transfer Required for the storage account.</span></span> 

1. <span data-ttu-id="f45b6-156">No portal do Azure, selecione **Criar Conta de Armazenamento** ou em uma conta de armazenamento existente, selecione **Configurações** e, em seguida, **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="f45b6-156">In the Azure portal, select **Create Storage Account**, or for an existing storage account, select **Settings** and then **Configuration**.</span></span>

2. <span data-ttu-id="f45b6-157">Em **Transferência Segura Obrigatória**, selecione **Habilitada**.</span><span class="sxs-lookup"><span data-stu-id="f45b6-157">Under **Secure Transfer Required**, select **Enabled**.</span></span>

![Criando uma conta de armazenamento](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

<span data-ttu-id="f45b6-159">Para obter instruções mais detalhadas, incluindo como habilitar o recurso Transferência Segura Obrigatória de forma programática, consulte [Exigir a Transferência Segura](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span><span class="sxs-lookup"><span data-stu-id="f45b6-159">For more detailed instructions, including how to enable Secure Transfer Required programmatically, see [Require Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span></span>

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a><span data-ttu-id="f45b6-160">Como fazer para criptografar dados no Armazenamento de Arquivos do Azure?</span><span class="sxs-lookup"><span data-stu-id="f45b6-160">How do I encrypt data in Azure File Storage?</span></span>

<span data-ttu-id="f45b6-161">Para criptografar dados em trânsito com o [Armazenamento de Arquivos do Azure](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), use o SMB 3.x com o Windows 8, 8.1 e 10 e com o Windows Server 2012 R2 e o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f45b6-161">To encrypt data in transit with [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), you can use SMB 3.x with Windows 8, 8.1, and 10 and with Windows Server 2012 R2 and Windows Server 2016.</span></span> <span data-ttu-id="f45b6-162">Quando você estiver usando o serviço de Arquivos do Azure, qualquer conexão sem criptografia falhará quando "Transferência segura obrigatória" estiver habilitada.</span><span class="sxs-lookup"><span data-stu-id="f45b6-162">When you are using the Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="f45b6-163">Isso inclui cenários usando SMB 2.1, SMB 3.0 sem criptografia e alguns tipos do cliente Linux SMB.</span><span class="sxs-lookup"><span data-stu-id="f45b6-163">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of the Linux SMB client.</span></span>

#### <a name="azure-client-side-encryption"></a><span data-ttu-id="f45b6-164">Criptografia do Lado do Cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="f45b6-164">Azure Client-Side Encryption</span></span>

<span data-ttu-id="f45b6-165">Outra opção para proteger dados pessoais enquanto estão sendo transferidos entre um aplicativo cliente e o Armazenamento do Azure é a [Criptografia do Lado do Cliente](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span><span class="sxs-lookup"><span data-stu-id="f45b6-165">Another option for protecting personal data while it’s being transferred between a client application and Azure Storage is [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span></span> <span data-ttu-id="f45b6-166">Os dados são criptografados antes de serem transferidos para o Armazenamento do Azure e, ao recuperar os dados no Armazenamento do Azure, eles são descriptografados depois de serem recebidos no lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="f45b6-166">The data is encrypted before being transferred into Azure Storage and when you retrieve the data from Azure Storage, the data is decrypted after it is received on the client side.</span></span>

### <a name="azure-site-to-site-vpn"></a><span data-ttu-id="f45b6-167">VPN site a site do Azure</span><span class="sxs-lookup"><span data-stu-id="f45b6-167">Azure Site-to-Site VPN</span></span>

<span data-ttu-id="f45b6-168">Uma maneira eficiente para proteger dados pessoais em trânsito entre uma rede corporativa ou um usuário e a rede virtual do Azure é usar uma VPN (Rede Virtual Privada) [site a site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) ou [ponto a site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal).</span><span class="sxs-lookup"><span data-stu-id="f45b6-168">An effective way to protect personal data in transit between a corporate network or user and the Azure virtual network is to use a [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) or [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) Virtual Private Network (VPN).</span></span> <span data-ttu-id="f45b6-169">Uma conexão VPN cria um túnel criptografado seguro pela Internet.</span><span class="sxs-lookup"><span data-stu-id="f45b6-169">A VPN connection creates a secure encrypted tunnel across the Internet.</span></span>

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a><span data-ttu-id="f45b6-170">Como fazer para criar uma conexão VPN site a site?</span><span class="sxs-lookup"><span data-stu-id="f45b6-170">How do I create a site-to-site VPN connection?</span></span>

<span data-ttu-id="f45b6-171">Uma VPN site a site conecta vários usuários na rede corporativa com o Azure.</span><span class="sxs-lookup"><span data-stu-id="f45b6-171">A site-to-site VPN connects multiple users on the corporate network to Azure.</span></span> <span data-ttu-id="f45b6-172">Para criar uma conexão site a site no portal do Azure, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f45b6-172">To create a site-to-site connection in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="f45b6-173">Crie uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f45b6-173">Create a virtual network.</span></span>

2. <span data-ttu-id="f45b6-174">Especifique um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="f45b6-174">Specify a DNS server.</span></span>

3. <span data-ttu-id="f45b6-175">Crie a sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="f45b6-175">Create the gateway subnet.</span></span>

4. <span data-ttu-id="f45b6-176">Crie o gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="f45b6-176">Create the VPN gateway.</span></span> 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. <span data-ttu-id="f45b6-177">Crie o gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="f45b6-177">Create the local network gateway.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. <span data-ttu-id="f45b6-178">Configure o dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="f45b6-178">Configure your VPN device.</span></span>

7. <span data-ttu-id="f45b6-179">Crie a conexão VPN.</span><span class="sxs-lookup"><span data-stu-id="f45b6-179">Create the VPN connection.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. <span data-ttu-id="f45b6-180">Verifique a conexão VPN.</span><span class="sxs-lookup"><span data-stu-id="f45b6-180">Verify the VPN connection.</span></span>

<span data-ttu-id="f45b6-181">Para obter instruções mais detalhadas sobre como criar uma conexão site a site no portal do Azure, consulte [Criar uma conexão Site a Site no Portal do Azure.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="f45b6-181">For more detailed instructions on how to create a site-to-site connection in the Azure portal, see [Create a Site-to-Site  connection in the Azure Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span></span>

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a><span data-ttu-id="f45b6-182">Como fazer para criar uma conexão VPN ponto a site?</span><span class="sxs-lookup"><span data-stu-id="f45b6-182">How do I create a point-to-site VPN connection?</span></span>

<span data-ttu-id="f45b6-183">Uma VPN Ponto a Site cria uma conexão segura de um computador cliente individual com uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f45b6-183">A Point-to-Site VPN creates a secure connection from an individual client computer to a virtual network.</span></span> <span data-ttu-id="f45b6-184">Isso é útil quando você deseja se conectar ao Azure em um local remoto, como de casa, um hotel ou um centro de conferências.</span><span class="sxs-lookup"><span data-stu-id="f45b6-184">This is useful when you  want to connect to Azure from a remote location, such as from home or a hotel or conference center.</span></span> <span data-ttu-id="f45b6-185">Para criar uma conexão ponto a site no portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="f45b6-185">To create a point-to-site  connection in the Azure portal,</span></span>

1. <span data-ttu-id="f45b6-186">Crie uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f45b6-186">Create a virtual network.</span></span>

2. <span data-ttu-id="f45b6-187">Adicione uma sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="f45b6-187">Add a gateway subnet.</span></span>

3. <span data-ttu-id="f45b6-188">Especifique um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="f45b6-188">Specify a DNS server.</span></span> <span data-ttu-id="f45b6-189">(opcional)</span><span class="sxs-lookup"><span data-stu-id="f45b6-189">(optional)</span></span>

4. <span data-ttu-id="f45b6-190">Crie um gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f45b6-190">Create a virtual network gateway.</span></span>

5. <span data-ttu-id="f45b6-191">Gere certificados.</span><span class="sxs-lookup"><span data-stu-id="f45b6-191">Generate certificates.</span></span>

6. <span data-ttu-id="f45b6-192">Adicione o pool de endereços de cliente.</span><span class="sxs-lookup"><span data-stu-id="f45b6-192">Add the client address pool.</span></span>

7. <span data-ttu-id="f45b6-193">Carregue os dados de certificado público do certificado raiz.</span><span class="sxs-lookup"><span data-stu-id="f45b6-193">Upload the root certificate public certificate data.</span></span>

8. <span data-ttu-id="f45b6-194">Gere e instale o pacote de configuração de cliente VPN.</span><span class="sxs-lookup"><span data-stu-id="f45b6-194">Generate and install the VPN client configuration package.</span></span>

9. <span data-ttu-id="f45b6-195">Instale um certificado do cliente exportado.</span><span class="sxs-lookup"><span data-stu-id="f45b6-195">Install an exported client certificate.</span></span>

10. <span data-ttu-id="f45b6-196">Conecte-se ao Azure.</span><span class="sxs-lookup"><span data-stu-id="f45b6-196">Connect to Azure.</span></span>

11. <span data-ttu-id="f45b6-197">Verifique a conexão.</span><span class="sxs-lookup"><span data-stu-id="f45b6-197">Verify your connection.</span></span>

<span data-ttu-id="f45b6-198">Para obter instruções mais detalhadas, consulte [Configurar uma conexão Ponto a Site a uma VNet usando a autenticação de certificado: Portal do Azure.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="f45b6-198">For more detailed instructions, see [Configure a Point-to-Site connection to a VNet using certificate authentication: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span></span>

### <a name="ssltls"></a><span data-ttu-id="f45b6-199">SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="f45b6-199">SSL/TLS</span></span>

<span data-ttu-id="f45b6-200">A Microsoft recomenda sempre usar protocolos SSL/TLS para a troca de dados em diferentes localizações.</span><span class="sxs-lookup"><span data-stu-id="f45b6-200">Microsoft recommends that you always use SSL/TLS protocols to exchange data across different locations.</span></span> <span data-ttu-id="f45b6-201">As organizações que optam por usar o [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) para mover conjuntos de dados grandes em um link de WAN dedicado de alta velocidade também podem criptografar os dados no nível do aplicativo usando o SSL/TLS ou outros protocolos para proteção extra.</span><span class="sxs-lookup"><span data-stu-id="f45b6-201">Organizations that choose to use [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) to move large data sets over a dedicated high-speed WAN link can also encrypt the data at the application-level using SSL/TLS or other protocols for added protection.</span></span>

### <a name="encryption-by-default"></a><span data-ttu-id="f45b6-202">Criptografia por padrão</span><span class="sxs-lookup"><span data-stu-id="f45b6-202">Encryption by default</span></span>

<span data-ttu-id="f45b6-203">A Microsoft usa a criptografia para proteger dados em trânsito entre clientes e serviços de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="f45b6-203">Microsoft uses encryption to protect data in transit between customers and Azure cloud services.</span></span> <span data-ttu-id="f45b6-204">Se você estiver interagindo com o Armazenamento do Azure pelo Portal do Azure, todas as transações ocorrerão via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f45b6-204">If you are interacting with Azure Storage through the Azure Portal, all transactions occur via HTTPS.</span></span>

<span data-ttu-id="f45b6-205">O [protocolo TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security) é o protocolo com o qual os data centers da Microsoft tentarão negociar com os sistemas cliente que se conectam aos serviços em nuvem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f45b6-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is the protocol that Microsoft data centers will attempt to negotiate with client systems that connect to Microsoft cloud services.</span></span> <span data-ttu-id="f45b6-206">O TLS fornece autenticação forte, privacidade de mensagem e integridade (habilita a detecção de adulteração, interceptação e falsificação de mensagens), interoperabilidade, flexibilidade de algoritmo, facilidade de implantação e uso.</span><span class="sxs-lookup"><span data-stu-id="f45b6-206">TLS provides strong authentication, message privacy, and integrity (enables detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, ease of deployment and use.</span></span>

<span data-ttu-id="f45b6-207">O [PFS](https://en.wikipedia.org/wiki/Forward_secrecy) (Perfect Forward Secrecy) também é utilizado para que cada conexão entre os sistemas cliente dos clientes e os serviços de nuvem da Microsoft usem chaves exclusivas.</span><span class="sxs-lookup"><span data-stu-id="f45b6-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is also employed so that each connection between customers’ client systems and Microsoft’s cloud services use unique keys.</span></span> <span data-ttu-id="f45b6-208">As conexões com os serviços em nuvem da Microsoft também aproveitam tamanhos de chave de criptografia de 2.048 bits baseada em RSA.</span><span class="sxs-lookup"><span data-stu-id="f45b6-208">Connections to Microsoft cloud services also take advantage of RSA based 2,048-bit encryption key lengths.</span></span> <span data-ttu-id="f45b6-209">A combinação do TLS, tamanhos de chave RSA de 2.048 bits e o PFS torna muito mais difícil para alguém interceptar e acessar dados em trânsito entre os clientes e os serviços em nuvem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f45b6-209">The combination of TLS, RSA 2,048-bit key lengths, and PFS makes it much  more difficult for someone to intercept and access data that is in transit between Microsoft cloud services and customers.</span></span>

<span data-ttu-id="f45b6-210">Os dados em trânsito são Always Encrypted no [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span><span class="sxs-lookup"><span data-stu-id="f45b6-210">Data in transit is always encrypted in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span></span> <span data-ttu-id="f45b6-211">Além de criptografar os dados antes de armazenar em mídia persistente, os dados são sempre protegidos em trânsito usando HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f45b6-211">In addition to encrypting data prior to storing to persistent media, the data is also always secured in transit by using HTTPS.</span></span> <span data-ttu-id="f45b6-212">HTTPS é o único protocolo com suporte para as interfaces REST do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f45b6-212">HTTPS is the only protocol that is supported for the Data Lake Store REST interfaces.</span></span>

## <a name="summary"></a><span data-ttu-id="f45b6-213">Resumo</span><span class="sxs-lookup"><span data-stu-id="f45b6-213">Summary</span></span>

<span data-ttu-id="f45b6-214">A empresa pode atingir sua meta de proteger dados pessoais e a privacidade desses dados impondo conexões HTTPS ao Armazenamento do Azure, usando Assinaturas de Acesso Compartilhado e habilitando o recurso Transferência Segura Obrigatória nas contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f45b6-214">The company can accomplish its goal of protecting personal data and the privacy of such data by enforcing HTTPS connections to Azure Storage, using Shared Access Signatures and enabling Secure Transfer Required on the storage accounts.</span></span> <span data-ttu-id="f45b6-215">Ela também pode proteger os dados pessoais usando conexões SMB 3.0 e implementando a criptografia do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="f45b6-215">They can also protect personal data by using SMB 3.0 connections and implementing client-side encryption.</span></span> <span data-ttu-id="f45b6-216">As conexões VPN site a site da rede corporativa para a rede virtual do Azure e as conexões VPN ponto a site dos usuários individuais criarão um túnel seguro por meio do qual os dados pessoais podem viajar com segurança.</span><span class="sxs-lookup"><span data-stu-id="f45b6-216">Site-to-site VPN connections from the corporate network to the Azure virtual network and point-to-site VPN connections from individual users will create a secure tunnel through which personal data can securely travel.</span></span> <span data-ttu-id="f45b6-217">As práticas de criptografia padrão da Microsoft protegem ainda mais a privacidade de dados pessoais.</span><span class="sxs-lookup"><span data-stu-id="f45b6-217">Microsoft’s default encryption practices will further protect the privacy of personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f45b6-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f45b6-218">Next steps</span></span>

- [<span data-ttu-id="f45b6-219">Melhores práticas de segurança de dados e criptografia do Azure</span><span class="sxs-lookup"><span data-stu-id="f45b6-219">Azure Data Security and Encryption Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [<span data-ttu-id="f45b6-220">Planejamento e design do Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="f45b6-220">Planning and design for VPN Gateway</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [<span data-ttu-id="f45b6-221">Perguntas frequentes de gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="f45b6-221">VPN Gateway FAQ</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [<span data-ttu-id="f45b6-222">Comprar e configurar um certificado SSL para o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="f45b6-222">Buy and configure an SSL Certificate for your Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
