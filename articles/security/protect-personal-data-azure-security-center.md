---
title: "Proteger dados pessoais com a Central de Segurança do Azure | Microsoft Docs"
description: "proteger dados pessoais usando a central de segurança do Azure"
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
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3a941389713a4d3dbffbbfe8a717409927d85c6d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="6232a-103">Proteger dados pessoais contra violações e ataques: Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="6232a-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="6232a-104">Este artigo ajudará você a entender como usar a Central de Segurança do Azure para proteger dados pessoais contra violações e ataques.</span><span class="sxs-lookup"><span data-stu-id="6232a-104">This article will help you understand how to use Azure Security Center to protect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="6232a-105">Cenário</span><span class="sxs-lookup"><span data-stu-id="6232a-105">Scenario</span></span> 

<span data-ttu-id="6232a-106">Uma empresa de cruzeiro de grande porte, com sede nos Estados Unidos, está expandindo suas operações para oferecer roteiros nos mares Mediterrâneo e Báltico, bem como nas Ilhas Britânicas.</span><span class="sxs-lookup"><span data-stu-id="6232a-106">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="6232a-107">Para ajudar nesses esforços, ela adquiriu várias linhas de cruzeiro menores localizadas na Itália, na Alemanha, na Dinamarca e no Reino Unido.</span><span class="sxs-lookup"><span data-stu-id="6232a-107">To help in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and the U.K.</span></span>

<span data-ttu-id="6232a-108">A empresa usa o Microsoft Azure para armazenar dados corporativos na nuvem.</span><span class="sxs-lookup"><span data-stu-id="6232a-108">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="6232a-109">Eles incluem informações de identificação pessoal, como nomes, endereços, números de telefone e informações de cartão de crédito.</span><span class="sxs-lookup"><span data-stu-id="6232a-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="6232a-110">Também incluem informações de Recursos Humanos, como:</span><span class="sxs-lookup"><span data-stu-id="6232a-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="6232a-111">Endereços</span><span class="sxs-lookup"><span data-stu-id="6232a-111">Addresses</span></span>
- <span data-ttu-id="6232a-112">Números de telefone</span><span class="sxs-lookup"><span data-stu-id="6232a-112">Phone numbers</span></span>
- <span data-ttu-id="6232a-113">Números de identificação fiscal</span><span class="sxs-lookup"><span data-stu-id="6232a-113">Tax identification numbers</span></span>
- <span data-ttu-id="6232a-114">Informações de saúde</span><span class="sxs-lookup"><span data-stu-id="6232a-114">Medical information</span></span>

<span data-ttu-id="6232a-115">A linha de cruzeiro também mantém um banco de dados grande de membros do programa de recompensa e fidelidade.</span><span class="sxs-lookup"><span data-stu-id="6232a-115">The cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="6232a-116">Os funcionários corporativos acessam a rede de escritórios remotos da empresa e os agentes de viagem localizados no mundo todo têm acesso a alguns recursos da empresa.</span><span class="sxs-lookup"><span data-stu-id="6232a-116">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources.</span></span>
<span data-ttu-id="6232a-117">Os dados pessoais viajam pela rede entre essas localizações e o data center da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6232a-117">Personal data travels across the network between these locations and the Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="6232a-118">Problema declarado</span><span class="sxs-lookup"><span data-stu-id="6232a-118">Problem statement</span></span>

<span data-ttu-id="6232a-119">A empresa se preocupa com a ameaça de ataques a seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6232a-119">The company is concerned about the threat of attacks on their Azure resources.</span></span> <span data-ttu-id="6232a-120">Ela deseja prevenir a exposição dos dados pessoais de clientes e funcionários a pessoas não autorizadas.</span><span class="sxs-lookup"><span data-stu-id="6232a-120">They want to prevent exposure of customers’ and employees’ personal data to unauthorized persons.</span></span> <span data-ttu-id="6232a-121">Também deseja obter diretrizes de prevenção e resposta/correção, bem como uma maneira eficaz de monitorar a segurança contínua de seus recursos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6232a-121">They want guidance on both prevention and response/remediation, as well as an effective way to monitor the ongoing security of their cloud resources.</span></span>
<span data-ttu-id="6232a-122">Ela precisa de uma linha forte de proteção contra os invasores sofisticados e organizados de hoje.</span><span class="sxs-lookup"><span data-stu-id="6232a-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="6232a-123">Meta da empresa</span><span class="sxs-lookup"><span data-stu-id="6232a-123">Company goal</span></span>

<span data-ttu-id="6232a-124">Uma das metas da empresa é garantir a privacidade dos dados pessoais de clientes e funcionários protegendo-os contra ameaças.</span><span class="sxs-lookup"><span data-stu-id="6232a-124">One of the company’s goals is to ensure the privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="6232a-125">Uma de suas metas é responder imediatamente aos sinais de violação para atenuar o impacto.</span><span class="sxs-lookup"><span data-stu-id="6232a-125">One of their goals is to respond immediately to signs of breach to mitigate the impact.</span></span> <span data-ttu-id="6232a-126">Ela precisa de uma maneira para avaliar o estado atual da segurança, identificar configurações vulneráveis e corrigi-las.</span><span class="sxs-lookup"><span data-stu-id="6232a-126">It requires a way to assess the current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="6232a-127">Soluções</span><span class="sxs-lookup"><span data-stu-id="6232a-127">Solutions</span></span>

<span data-ttu-id="6232a-128">O ASC (Central de Segurança do Microsoft Azure) fornece uma solução integrada de gerenciamento de política e monitoramento da segurança.</span><span class="sxs-lookup"><span data-stu-id="6232a-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="6232a-129">Ele oferece funcionalidades eficazes e fáceis de usar de prevenção, detecção e resposta a ameaças.</span><span class="sxs-lookup"><span data-stu-id="6232a-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="6232a-130">Prevenção</span><span class="sxs-lookup"><span data-stu-id="6232a-130">Prevention</span></span>

<span data-ttu-id="6232a-131">O ASC ajuda a prevenir violações, permitindo definir políticas de segurança, fornecer acesso Just-In-Time e implementar recomendações de segurança.</span><span class="sxs-lookup"><span data-stu-id="6232a-131">ASC helps you prevent breaches by enabling you to set security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="6232a-132">Uma política de segurança define o conjunto de controles recomendados para os recursos na assinatura especificada.</span><span class="sxs-lookup"><span data-stu-id="6232a-132">A security policy defines the set of controls recommended for resources within the specified subscription.</span></span> <span data-ttu-id="6232a-133">O acesso Just-In-Time pode ser usado para bloquear o tráfego de entrada nas VMs do Azure, reduzindo a exposição a ataques.</span><span class="sxs-lookup"><span data-stu-id="6232a-133">Just in time access can be used to lock down inbound traffic to your Azure VMs, reducing exposure to attacks.</span></span> <span data-ttu-id="6232a-134">Recomendações de segurança são criadas pelo ASC depois de analisar o estado de segurança dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6232a-134">Security recommendations are created by ASC after analyzing the security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="6232a-135">Como fazer para definir políticas de segurança no ASC?</span><span class="sxs-lookup"><span data-stu-id="6232a-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="6232a-136">É possível configurar políticas de segurança para cada assinatura.</span><span class="sxs-lookup"><span data-stu-id="6232a-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="6232a-137">Para modificar uma política de segurança, você deve ser um proprietário ou colaborador dessa assinatura.</span><span class="sxs-lookup"><span data-stu-id="6232a-137">To modify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="6232a-138">No portal do Azure, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6232a-138">In the Azure portal, do the following:</span></span>

1. <span data-ttu-id="6232a-139">Selecione **Política** no painel do ASC.</span><span class="sxs-lookup"><span data-stu-id="6232a-139">Select **Policy** in the ASC dashboard.</span></span>

2. <span data-ttu-id="6232a-140">Selecione a assinatura na qual você deseja habilitar a política.</span><span class="sxs-lookup"><span data-stu-id="6232a-140">Select the subscription on which you want to enable the policy.</span></span>

3. <span data-ttu-id="6232a-141">Escolha **Política prevenção** para configurar as políticas por assinatura.</span><span class="sxs-lookup"><span data-stu-id="6232a-141">Choose **Prevention policy** to configure policies per subscription.</span></span> <span data-ttu-id="6232a-142">A opção **Coletar dados de máquinas virtuais** deve ser definida como **Ativado.**</span><span class="sxs-lookup"><span data-stu-id="6232a-142">**Collect data from virtual machines** should be set to **On.**</span></span>

4. <span data-ttu-id="6232a-143">Nas opções de **Política de prevenção**, selecione **Ativado** para habilitar as recomendações de segurança que são relevantes para a assinatura.</span><span class="sxs-lookup"><span data-stu-id="6232a-143">In the **Prevention policy** options, select **On** to enable the security recommendations that are relevant for the subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="6232a-144">Para obter instruções mais detalhadas e uma explicação de cada uma das recomendações de política que podem ser habilitadas, consulte [Definir políticas de segurança na Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span><span class="sxs-lookup"><span data-stu-id="6232a-144">For more detailed instructions and an explanation of each of the policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="6232a-145">Como fazer para configurar o acesso JIT (Just-In-Time)?</span><span class="sxs-lookup"><span data-stu-id="6232a-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="6232a-146">Quando o JIT está habilitado, a Central de Segurança bloqueia o tráfego de entrada às VMs do Azure, criando uma regra do NSG.</span><span class="sxs-lookup"><span data-stu-id="6232a-146">When JIT is enabled, Security Center locks down inbound traffic to your Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="6232a-147">Você seleciona as portas na VM para as quais o tráfego de entrada será bloqueado.</span><span class="sxs-lookup"><span data-stu-id="6232a-147">You select the ports on the VM to which inbound traffic will be locked down.</span></span> <span data-ttu-id="6232a-148">Para usar o acesso JIT, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6232a-148">To use JIT access, do the following:</span></span>

1. <span data-ttu-id="6232a-149">Selecione o **bloco de acesso de VM Just-In-Time** na folha do ASC.</span><span class="sxs-lookup"><span data-stu-id="6232a-149">Select the **Just in time VM access tile** on the ASC blade.</span></span>

2. <span data-ttu-id="6232a-150">Selecione a guia **Recomendado**.</span><span class="sxs-lookup"><span data-stu-id="6232a-150">Select the **Recommended** tab.</span></span>

3. <span data-ttu-id="6232a-151">Em **VMs**, selecione as VMs que você deseja habilitar.</span><span class="sxs-lookup"><span data-stu-id="6232a-151">Under **VMs**, select the VMs that you want to enable.</span></span> <span data-ttu-id="6232a-152">Isso coloca uma marca de seleção ao lado de uma VM.</span><span class="sxs-lookup"><span data-stu-id="6232a-152">This puts a checkmark next to a VM.</span></span> 
4. <span data-ttu-id="6232a-153">Selecione **Habilitar JIT** nas VMs.</span><span class="sxs-lookup"><span data-stu-id="6232a-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="6232a-154">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6232a-154">Select **Save**.</span></span>

<span data-ttu-id="6232a-155">Em seguida, você pode ver as portas padrão que o ASC recomenda que sejam habilitadas para o JIT.</span><span class="sxs-lookup"><span data-stu-id="6232a-155">Then you can see the default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="6232a-156">Também adicione e configure uma nova porta na qual você deseja habilitar a solução Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="6232a-156">You can also add and configure a new port on which you want to enable the just in time solution.</span></span> <span data-ttu-id="6232a-157">O bloco **Acesso de VM Just-In-Time** na Central de Segurança mostra o número de VMs configuradas para o acesso JIT.</span><span class="sxs-lookup"><span data-stu-id="6232a-157">The **Just in time VM access** tile in the Security Center shows the number of VMs configured for JIT access.</span></span> <span data-ttu-id="6232a-158">Ele também mostra o número de solicitações de acesso aprovadas feitas na última semana.</span><span class="sxs-lookup"><span data-stu-id="6232a-158">It also shows the number of approved access requests made in the last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="6232a-159">Para obter instruções sobre como fazer isso, além de mais informações sobre o acesso Just-In-Time, consulte [Gerenciar o acesso de máquina virtual usando o Just-In-Time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span><span class="sxs-lookup"><span data-stu-id="6232a-159">For instructions on how to do this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="6232a-160">Como fazer para implementar as recomendações de segurança do ASC?</span><span class="sxs-lookup"><span data-stu-id="6232a-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="6232a-161">Quando a Central de Segurança identifica possíveis vulnerabilidades de segurança, cria recomendações.</span><span class="sxs-lookup"><span data-stu-id="6232a-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="6232a-162">As recomendações o orientam ao longo do processo de configuração dos controles necessários.</span><span class="sxs-lookup"><span data-stu-id="6232a-162">The recommendations guide you through the process of configuring the needed controls.</span></span> 
1. <span data-ttu-id="6232a-163">Selecione o bloco **Recomendações** no painel do ASC.</span><span class="sxs-lookup"><span data-stu-id="6232a-163">Select the **Recommendations** tile on the ASC dashboard.</span></span>

2. <span data-ttu-id="6232a-164">Exiba as recomendações, que são mostradas em um formato de tabela, em que cada linha representa uma recomendação.</span><span class="sxs-lookup"><span data-stu-id="6232a-164">View the recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="6232a-165">Para filtrar recomendações, selecione **Filtrar** e selecione os valores de gravidade e estado que você deseja ver.</span><span class="sxs-lookup"><span data-stu-id="6232a-165">To filter recommendations, select **Filter** and select the severity and state values you wish to see.</span></span>

4. <span data-ttu-id="6232a-166">Para ignorar uma recomendação que não é aplicável, clique com o botão direito do mouse e selecione **Ignorar.**</span><span class="sxs-lookup"><span data-stu-id="6232a-166">To dismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="6232a-167">Avalie qual recomendação deve ser aplicada primeiro.</span><span class="sxs-lookup"><span data-stu-id="6232a-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="6232a-168">Aplique as recomendações em ordem de prioridade.</span><span class="sxs-lookup"><span data-stu-id="6232a-168">Apply the recommendations in order of priority.</span></span>

<span data-ttu-id="6232a-169">Para obter uma lista de possíveis recomendações e passos a passos sobre como aplicar cada uma, consulte [Gerenciando recomendações de segurança na Central de Segurança do Azure.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span><span class="sxs-lookup"><span data-stu-id="6232a-169">For a list of possible recommendations and walk-throughs on how to apply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="6232a-170">Detecção e resposta</span><span class="sxs-lookup"><span data-stu-id="6232a-170">Detection and Response</span></span>

<span data-ttu-id="6232a-171">A detecção e resposta funcionam juntas, quando você deseja responder o mais rápido possível após a detecção de uma ameaça.</span><span class="sxs-lookup"><span data-stu-id="6232a-171">Detection and response go together, as you want to respond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="6232a-172">A detecção de ameaças do ASC funciona com a coleta automática das informações de segurança dos recursos do Azure, da rede e das soluções de parceiros conectados.</span><span class="sxs-lookup"><span data-stu-id="6232a-172">ASC threat detection works by automatically collecting security information from your Azure resources, the network, and connected partner solutions.</span></span> <span data-ttu-id="6232a-173">O ASC pode atualizar rapidamente seus algoritmos de detecção conforme os invasores lançam explorações novas e cada vez mais sofisticadas.</span><span class="sxs-lookup"><span data-stu-id="6232a-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="6232a-174">Para obter informações mais detalhadas sobre como funciona a detecção de ameaças do ASC, consulte [Funcionalidades de detecção da Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span><span class="sxs-lookup"><span data-stu-id="6232a-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-to-security-alerts"></a><span data-ttu-id="6232a-175">Como fazer para gerenciar e responder a alertas de segurança?</span><span class="sxs-lookup"><span data-stu-id="6232a-175">How do I manage and respond to security alerts?</span></span>

<span data-ttu-id="6232a-176">Uma lista de alertas de segurança priorizados é mostrada na Central de Segurança, junto com as informações necessárias para investigar rapidamente o problema.</span><span class="sxs-lookup"><span data-stu-id="6232a-176">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem.</span></span> <span data-ttu-id="6232a-177">A Central de Segurança também inclui recomendações sobre como corrigir um ataque.</span><span class="sxs-lookup"><span data-stu-id="6232a-177">Security Center also includes recommendations for how to remediate an attack.</span></span> <span data-ttu-id="6232a-178">Para gerenciar os alertas de segurança, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6232a-178">To manage your security alerts, do the following:</span></span>

1. <span data-ttu-id="6232a-179">Selecione o bloco **Alertas de segurança** no painel do ASC.</span><span class="sxs-lookup"><span data-stu-id="6232a-179">Select the **Security alerts** tile in the ASC dashboard.</span></span> <span data-ttu-id="6232a-180">Isso mostra detalhes de cada alerta.</span><span class="sxs-lookup"><span data-stu-id="6232a-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="6232a-181">Para filtrar os alertas com base na data, no estado e na gravidade, selecione **Filtrar** e, em seguida, os valores que você deseja ver.</span><span class="sxs-lookup"><span data-stu-id="6232a-181">To filter alerts based on date, state, and severity, select **Filter** and then select the values you want to see.</span></span>

3. <span data-ttu-id="6232a-182">Para responder a um alerta, selecione-o, examine as informações e, em seguida, selecione o recurso que foi atacado.</span><span class="sxs-lookup"><span data-stu-id="6232a-182">To respond to an alert, select it and review the information, then select the resource that was attacked.</span></span>

4. <span data-ttu-id="6232a-183">No campo **Descrição**, você verá os detalhes, incluindo a correção recomendada.</span><span class="sxs-lookup"><span data-stu-id="6232a-183">In the **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="6232a-184">Para obter instruções mais detalhadas sobre como responder a alertas de segurança, consulte [Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span><span class="sxs-lookup"><span data-stu-id="6232a-184">For more detailed instructions on responding to security alerts, see [Managing and responding to security alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="6232a-185">Para obter ajuda na investigação de alertas de segurança, a empresa pode integrar os alertas do ASC à sua própria solução SIEM, usando a [Integração de Logs do Azure](https://aka.ms/AzLog).</span><span class="sxs-lookup"><span data-stu-id="6232a-185">For further help in investigating security alerts, the company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="6232a-186">Como fazer para gerenciar incidentes de segurança?</span><span class="sxs-lookup"><span data-stu-id="6232a-186">How do I manage security incidents?</span></span>

<span data-ttu-id="6232a-187">No ASC, um incidente de segurança é uma agregação de todos os alertas de um recurso que se alinham com os padrões da cadeia de encerramento.</span><span class="sxs-lookup"><span data-stu-id="6232a-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="6232a-188">Um Incidente revelará a lista de alertas relacionados, o que permite a obtenção de mais informações sobre cada ocorrência.</span><span class="sxs-lookup"><span data-stu-id="6232a-188">An Incident will reveal the list of related alerts, which enables you to obtain more information about each occurrence.</span></span> <span data-ttu-id="6232a-189">Os incidentes são exibidos no bloco e na folha Alertas de Segurança.</span><span class="sxs-lookup"><span data-stu-id="6232a-189">Incidents appear in the Security Alerts tile and blade.</span></span>

<span data-ttu-id="6232a-190">Para examinar e gerenciar incidentes de segurança, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6232a-190">To review and manage security incidents, do the following:</span></span>

1. <span data-ttu-id="6232a-191">Selecione o bloco **Alertas de segurança**.</span><span class="sxs-lookup"><span data-stu-id="6232a-191">Select the **Security alerts** tile.</span></span> <span data-ttu-id="6232a-192">Se um incidente de segurança for detectado, ele será exibido no gráfico de alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="6232a-192">if a security incident is detected, it will appear under the security alerts graph.</span></span> <span data-ttu-id="6232a-193">Ele terá um ícone diferente dos outros alertas.</span><span class="sxs-lookup"><span data-stu-id="6232a-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="6232a-194">Selecione o incidente para ver mais detalhes sobre esse incidente de segurança.</span><span class="sxs-lookup"><span data-stu-id="6232a-194">Select the incident to see more details about this security incident.</span></span> <span data-ttu-id="6232a-195">Detalhes adicionais incluem sua descrição completa, sua gravidade, seu estado atual, o recurso atacado, as etapas de correção do incidente e os alertas que foram incluídos nesse incidente.</span><span class="sxs-lookup"><span data-stu-id="6232a-195">Additional details include its full description, its severity, its current state, the attacked resource, the remediation steps for the incident, and the alerts that were included in this incident.</span></span>

<span data-ttu-id="6232a-196">Filtre para ver **somente incidentes**, **somente alertas** ou **ambos**.</span><span class="sxs-lookup"><span data-stu-id="6232a-196">You can filter to see **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-the-threat-intelligence-report"></a><span data-ttu-id="6232a-197">Como fazer para acessar o Relatório de Inteligência contra Ameaças?</span><span class="sxs-lookup"><span data-stu-id="6232a-197">How do I access the Threat Intelligence Report?</span></span>

<span data-ttu-id="6232a-198">O ASC analisa informações de várias fontes para identificar ameaças.</span><span class="sxs-lookup"><span data-stu-id="6232a-198">ASC analyzes information from multiple sources to identify threats.</span></span> <span data-ttu-id="6232a-199">Para ajudar as equipes de resposta a incidentes a investigar e a corrigir ameaças, a Central de Segurança inclui um relatório de inteligência contra ameaças que contém informações sobre a ameaça detectada.</span><span class="sxs-lookup"><span data-stu-id="6232a-199">To assist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about the threat that was detected.</span></span>

<span data-ttu-id="6232a-200">A Central de Segurança tem três tipos de relatórios de ameaça, que podem variar de acordo com o ataque.</span><span class="sxs-lookup"><span data-stu-id="6232a-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="6232a-201">Os relatórios disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="6232a-201">The reports available are:</span></span>

- <span data-ttu-id="6232a-202">Relatório de Grupo de Atividade: fornece análises avançadas sobre os invasores, seus objetivos e táticas.</span><span class="sxs-lookup"><span data-stu-id="6232a-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="6232a-203">Relatório de Campanha: concentra-se nos detalhes de campanhas de ataque específicas.</span><span class="sxs-lookup"><span data-stu-id="6232a-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="6232a-204">Relatório de Resumo de Ameaças: abrange todos os itens dos dois relatórios anteriores.</span><span class="sxs-lookup"><span data-stu-id="6232a-204">Threat Summary Report: covers all items in the previous two reports.</span></span>

<span data-ttu-id="6232a-205">Esse tipo de informação é muito útil durante o processo de resposta a incidentes, em que há uma investigação em andamento para compreender a origem do ataque, as motivações do invasor e o que fazer para atenuar esse problema no futuro.</span><span class="sxs-lookup"><span data-stu-id="6232a-205">This type of information is very useful during the incident response process, where there is an ongoing investigation to understand the source of the attack, the attacker’s motivations, and what to do to mitigate this issue moving forward.</span></span>

1. <span data-ttu-id="6232a-206">Para acessar o relatório de inteligência contra ameaças, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6232a-206">To access the threat intelligence report, do the following:</span></span>

2. <span data-ttu-id="6232a-207">Selecione o bloco **Alertas de segurança** no painel do ASC.</span><span class="sxs-lookup"><span data-stu-id="6232a-207">Select the **Security alerts** tile on the ASC dashboard.</span></span>

3. <span data-ttu-id="6232a-208">Selecione o alerta de segurança do qual você deseja obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="6232a-208">Select the security alert for which you want to obtain more information.</span></span>

4. <span data-ttu-id="6232a-209">No campo **Relatórios**, clique no link para o relatório de inteligência contra ameaças.</span><span class="sxs-lookup"><span data-stu-id="6232a-209">In the **Reports** field, click the link to the threat intelligence report.</span></span>

5. <span data-ttu-id="6232a-210">Isso abrirá o arquivo PDF, que pode ser baixado.</span><span class="sxs-lookup"><span data-stu-id="6232a-210">This will open the PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="6232a-211">Para obter mais informações sobre o relatório de inteligência contra ameaças do ASC, consulte [Relatório de Inteligência contra Ameaças da Central de Segurança do Azure.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="6232a-211">For additional information about the ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="6232a-212">Avaliação</span><span class="sxs-lookup"><span data-stu-id="6232a-212">Assessment</span></span>

<span data-ttu-id="6232a-213">Para ajudar no teste, na avaliação e na avaliação de sua postura de segurança, o ASC fornece uma avaliação de vulnerabilidade integrada com agentes de nuvem Qualys, como parte de seu componente de recomendações de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6232a-213">To help with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="6232a-214">O agente Qualys relata os dados de vulnerabilidade para a plataforma de gerenciamento do Qualys, que, por sua vez, envia os dados de monitoramento de integridade e vulnerabilidade novamente para o ASC.</span><span class="sxs-lookup"><span data-stu-id="6232a-214">The Qualys agent reports vulnerability data to the Qualys management platform, which then sends vulnerability and health monitoring data back to ASC.</span></span> <span data-ttu-id="6232a-215">A recomendação para adicionar uma solução de avaliação de vulnerabilidade é exibida na folha **Recomendações** do painel do ASC.</span><span class="sxs-lookup"><span data-stu-id="6232a-215">The recommendation to add a vulnerability assessment solution is displayed in the **Recommendations** blade on the ASC dashboard.</span></span>

<span data-ttu-id="6232a-216">Após a instalação da solução de avaliação de vulnerabilidade na VM de destino, a Central de Segurança examinará a VM para detectar e identificar vulnerabilidades de aplicativos e do sistema.</span><span class="sxs-lookup"><span data-stu-id="6232a-216">After the vulnerability assessment solution is installed on the target VM, Security Center scans the VM to detect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="6232a-217">Os problemas detectados são exibidos na opção **Recomendações de Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="6232a-217">Detected issues are shown under the **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="6232a-218">Como fazer para implementar uma solução de avaliação de vulnerabilidade?</span><span class="sxs-lookup"><span data-stu-id="6232a-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="6232a-219">Se uma Máquina Virtual não tem uma solução de avaliação de vulnerabilidade integrada já implantada, a Central de Segurança recomenda que ela seja instalada.</span><span class="sxs-lookup"><span data-stu-id="6232a-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="6232a-220">No painel do ASC, na folha **Recomendações**, selecione **Adicionar uma solução de avaliação de vulnerabilidade.**</span><span class="sxs-lookup"><span data-stu-id="6232a-220">In the ASC dashboard, on the **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="6232a-221">Selecione as VMs em que você deseja instalar a solução de avaliação de vulnerabilidade.</span><span class="sxs-lookup"><span data-stu-id="6232a-221">Select the VMs where you want to install the vulnerability assessment solution.</span></span>

3. <span data-ttu-id="6232a-222">Clique em **Instalar em [número de] VMs.**</span><span class="sxs-lookup"><span data-stu-id="6232a-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="6232a-223">Selecione uma solução de parceiro no Azure Marketplace ou, em **Usar solução existente**, selecione **Qualys.**</span><span class="sxs-lookup"><span data-stu-id="6232a-223">Select a partner solution in the Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="6232a-224">Ative ou desative as configurações de atualização automática na folha **Soluções de Parceiros**.</span><span class="sxs-lookup"><span data-stu-id="6232a-224">You can turn the auto update settings on or off in the **Partner Solutions** blade.</span></span>

<span data-ttu-id="6232a-225">Para obter mais instruções sobre como implementar uma solução de avaliação de vulnerabilidade, consulte [Avaliação de vulnerabilidade na Central de Segurança do Azure.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span><span class="sxs-lookup"><span data-stu-id="6232a-225">For further instructions on how to implement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6232a-226">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6232a-226">Next steps</span></span>

- [<span data-ttu-id="6232a-227">Guia de início rápido da Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="6232a-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="6232a-228">Introdução à Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="6232a-228">Introduction to Azure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="6232a-229">Integrando alertas da Central de Segurança do Azure com a integração de logs do Azure</span><span class="sxs-lookup"><span data-stu-id="6232a-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [<span data-ttu-id="6232a-230">Melhorar a Central de Segurança do Azure com a avaliação de vulnerabilidade integrada</span><span class="sxs-lookup"><span data-stu-id="6232a-230">Boost Azure Security Center with Integrated Vulnerability Assessment</span></span>](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
