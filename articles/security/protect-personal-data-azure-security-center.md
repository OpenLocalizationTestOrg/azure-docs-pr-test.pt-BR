---
title: "dados pessoais de aaaProtect na Central de segurança do Azure | Microsoft Docs"
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
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="8054f-103">Proteger dados pessoais contra violações e ataques: Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="8054f-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="8054f-104">Este artigo ajuda você a entender como os dados pessoais do toouse Central de segurança do Azure tooprotect de violar e ataques.</span><span class="sxs-lookup"><span data-stu-id="8054f-104">This article will help you understand how toouse Azure Security Center tooprotect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="8054f-105">Cenário</span><span class="sxs-lookup"><span data-stu-id="8054f-105">Scenario</span></span> 

<span data-ttu-id="8054f-106">Uma empresa cruzeiro grandes, com sede em Olá Estados Unidos, está expandindo suas roteiros de toooffer operações Olá Mediterrâneo e mares báltico, bem como Olá Britânicas.</span><span class="sxs-lookup"><span data-stu-id="8054f-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="8054f-107">toohelp nesses esforços, ela adquiriu várias linhas de cruzeiro menores com base na Itália, Alemanha, Dinamarca e Olá Reino Unido</span><span class="sxs-lookup"><span data-stu-id="8054f-107">toohelp in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="8054f-108">empresa de saudação usa dados corporativos do Microsoft Azure toostore na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="8054f-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="8054f-109">Eles incluem informações de identificação pessoal, como nomes, endereços, números de telefone e informações de cartão de crédito.</span><span class="sxs-lookup"><span data-stu-id="8054f-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="8054f-110">Também incluem informações de Recursos Humanos, como:</span><span class="sxs-lookup"><span data-stu-id="8054f-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="8054f-111">Endereços</span><span class="sxs-lookup"><span data-stu-id="8054f-111">Addresses</span></span>
- <span data-ttu-id="8054f-112">Números de telefone</span><span class="sxs-lookup"><span data-stu-id="8054f-112">Phone numbers</span></span>
- <span data-ttu-id="8054f-113">Números de identificação fiscal</span><span class="sxs-lookup"><span data-stu-id="8054f-113">Tax identification numbers</span></span>
- <span data-ttu-id="8054f-114">Informações de saúde</span><span class="sxs-lookup"><span data-stu-id="8054f-114">Medical information</span></span>

<span data-ttu-id="8054f-115">linha de cruzeiro Olá também mantém um banco de dados grande de membros do programa de recompensa e fidelidade.</span><span class="sxs-lookup"><span data-stu-id="8054f-115">hello cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="8054f-116">Os funcionários corporativos acesso Olá rede da empresa Olá escritórios remotos e agentes espalhados Olá, mundo têm acesso toosome recursos da empresa.</span><span class="sxs-lookup"><span data-stu-id="8054f-116">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>
<span data-ttu-id="8054f-117">Dados pessoais viajam pela rede Olá entre esses locais e o data center da Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="8054f-117">Personal data travels across hello network between these locations and hello Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="8054f-118">Problema declarado</span><span class="sxs-lookup"><span data-stu-id="8054f-118">Problem statement</span></span>

<span data-ttu-id="8054f-119">empresa de saudação está preocupada a ameaça de saudação de ataques a seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8054f-119">hello company is concerned about hello threat of attacks on their Azure resources.</span></span> <span data-ttu-id="8054f-120">Eles querem tooprevent exposição de pessoas de toounauthorized dados pessoais dos funcionários e clientes.</span><span class="sxs-lookup"><span data-stu-id="8054f-120">They want tooprevent exposure of customers’ and employees’ personal data toounauthorized persons.</span></span> <span data-ttu-id="8054f-121">Eles desejam obter orientação sobre a prevenção e resposta/correção, bem como uma maneira eficiente toomonitor Olá contínuo de segurança de seus recursos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="8054f-121">They want guidance on both prevention and response/remediation, as well as an effective way toomonitor hello ongoing security of their cloud resources.</span></span>
<span data-ttu-id="8054f-122">Ela precisa de uma linha forte de proteção contra os invasores sofisticados e organizados de hoje.</span><span class="sxs-lookup"><span data-stu-id="8054f-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="8054f-123">Meta da empresa</span><span class="sxs-lookup"><span data-stu-id="8054f-123">Company goal</span></span>

<span data-ttu-id="8054f-124">Uma das metas da empresa Olá é privacidade de saudação tooensure dos dados pessoais dos funcionários e clientes protegê-lo contra ameaças.</span><span class="sxs-lookup"><span data-stu-id="8054f-124">One of hello company’s goals is tooensure hello privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="8054f-125">Um dos seus objetivos é toorespond imediatamente toosigns de violação toomitigate Olá impacto.</span><span class="sxs-lookup"><span data-stu-id="8054f-125">One of their goals is toorespond immediately toosigns of breach toomitigate hello impact.</span></span> <span data-ttu-id="8054f-126">Requer uma maneira tooassess Olá estado atual da segurança, identificar configurações vulneráveis e corrigi-los.</span><span class="sxs-lookup"><span data-stu-id="8054f-126">It requires a way tooassess hello current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="8054f-127">Soluções</span><span class="sxs-lookup"><span data-stu-id="8054f-127">Solutions</span></span>

<span data-ttu-id="8054f-128">O ASC (Central de Segurança do Microsoft Azure) fornece uma solução integrada de gerenciamento de política e monitoramento da segurança.</span><span class="sxs-lookup"><span data-stu-id="8054f-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="8054f-129">Ele oferece funcionalidades eficazes e fáceis de usar de prevenção, detecção e resposta a ameaças.</span><span class="sxs-lookup"><span data-stu-id="8054f-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="8054f-130">Prevenção</span><span class="sxs-lookup"><span data-stu-id="8054f-130">Prevention</span></span>

<span data-ttu-id="8054f-131">ASC ajuda a evitar violações, permitindo que você tooset as políticas de segurança, forneça acesso just-in-time e implementar as recomendações de segurança.</span><span class="sxs-lookup"><span data-stu-id="8054f-131">ASC helps you prevent breaches by enabling you tooset security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="8054f-132">Uma política de segurança define o conjunto de saudação de controles recomendado para recursos em Olá especificado assinatura.</span><span class="sxs-lookup"><span data-stu-id="8054f-132">A security policy defines hello set of controls recommended for resources within hello specified subscription.</span></span> <span data-ttu-id="8054f-133">No momento o acesso pode ser usado toolock para baixo tráfego de entrada tooyour VMs do Azure, reduzindo a exposição tooattacks.</span><span class="sxs-lookup"><span data-stu-id="8054f-133">Just in time access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks.</span></span> <span data-ttu-id="8054f-134">Recomendações de segurança são criadas pelo ASC depois de analisar o estado de segurança Olá seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8054f-134">Security recommendations are created by ASC after analyzing hello security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="8054f-135">Como fazer para definir políticas de segurança no ASC?</span><span class="sxs-lookup"><span data-stu-id="8054f-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="8054f-136">É possível configurar políticas de segurança para cada assinatura.</span><span class="sxs-lookup"><span data-stu-id="8054f-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="8054f-137">toomodify uma política de segurança, você deve ser um proprietário ou colaborador da assinatura.</span><span class="sxs-lookup"><span data-stu-id="8054f-137">toomodify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="8054f-138">No portal do Azure de Olá, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="8054f-138">In hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="8054f-139">Selecione **política** no painel de controle do hello ASC.</span><span class="sxs-lookup"><span data-stu-id="8054f-139">Select **Policy** in hello ASC dashboard.</span></span>

2. <span data-ttu-id="8054f-140">Selecione a assinatura de saudação no qual você deseja tooenable política de saudação.</span><span class="sxs-lookup"><span data-stu-id="8054f-140">Select hello subscription on which you want tooenable hello policy.</span></span>

3. <span data-ttu-id="8054f-141">Escolha **política de prevenção de** tooconfigure políticas por assinatura.</span><span class="sxs-lookup"><span data-stu-id="8054f-141">Choose **Prevention policy** tooconfigure policies per subscription.</span></span> <span data-ttu-id="8054f-142">**Coletar dados de máquinas virtuais** deve ser definido muito**em.**</span><span class="sxs-lookup"><span data-stu-id="8054f-142">**Collect data from virtual machines** should be set too**On.**</span></span>

4. <span data-ttu-id="8054f-143">Em Olá **política de prevenção de** opções, selecionadas **na** tooenable Olá as recomendações de segurança que são relevantes para a assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="8054f-143">In hello **Prevention policy** options, select **On** tooenable hello security recommendations that are relevant for hello subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="8054f-144">Para obter mais instruções e uma explicação de cada uma das recomendações de política de saudação que podem ser habilitadas, consulte [definir políticas de segurança na Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span><span class="sxs-lookup"><span data-stu-id="8054f-144">For more detailed instructions and an explanation of each of hello policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="8054f-145">Como fazer para configurar o acesso JIT (Just-In-Time)?</span><span class="sxs-lookup"><span data-stu-id="8054f-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="8054f-146">Quando JIT está habilitada, a Central de segurança bloqueia o tráfego de entrada tooyour VMs do Azure, criando uma regra NSG.</span><span class="sxs-lookup"><span data-stu-id="8054f-146">When JIT is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="8054f-147">Selecione as portas de saudação em Olá VM toowhich o tráfego de entrada será bloqueado para baixo.</span><span class="sxs-lookup"><span data-stu-id="8054f-147">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="8054f-148">toouse JIT acessar, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="8054f-148">toouse JIT access, do hello following:</span></span>

1. <span data-ttu-id="8054f-149">Selecione Olá **logo no bloco de acesso VM tempo** na folha ASC hello.</span><span class="sxs-lookup"><span data-stu-id="8054f-149">Select hello **Just in time VM access tile** on hello ASC blade.</span></span>

2. <span data-ttu-id="8054f-150">Selecione Olá **recomendado** guia.</span><span class="sxs-lookup"><span data-stu-id="8054f-150">Select hello **Recommended** tab.</span></span>

3. <span data-ttu-id="8054f-151">Em **VMs**, selecione Olá VMs que você deseja tooenable.</span><span class="sxs-lookup"><span data-stu-id="8054f-151">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="8054f-152">Isso coloca uma tooa de marca de seleção próxima VM.</span><span class="sxs-lookup"><span data-stu-id="8054f-152">This puts a checkmark next tooa VM.</span></span> 
4. <span data-ttu-id="8054f-153">Selecione **Habilitar JIT** nas VMs.</span><span class="sxs-lookup"><span data-stu-id="8054f-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="8054f-154">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8054f-154">Select **Save**.</span></span>

<span data-ttu-id="8054f-155">Em seguida, você pode ver as portas padrão Olá ASC recomenda habilitar de JIT.</span><span class="sxs-lookup"><span data-stu-id="8054f-155">Then you can see hello default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="8054f-156">Você também pode adicionar e configurar uma nova porta na qual você deseja tooenable Olá apenas na solução de tempo.</span><span class="sxs-lookup"><span data-stu-id="8054f-156">You can also add and configure a new port on which you want tooenable hello just in time solution.</span></span> <span data-ttu-id="8054f-157">Olá **apenas no acesso de tempo de VM** lado a lado na Central de segurança de saudação mostra o número de saudação de máquinas virtuais configuradas para acesso JIT.</span><span class="sxs-lookup"><span data-stu-id="8054f-157">hello **Just in time VM access** tile in hello Security Center shows hello number of VMs configured for JIT access.</span></span> <span data-ttu-id="8054f-158">Ele também mostra o número de Olá aprovados de solicitações de acesso feitas no hello última semana.</span><span class="sxs-lookup"><span data-stu-id="8054f-158">It also shows hello number of approved access requests made in hello last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="8054f-159">Para obter instruções sobre como toodo, e informações adicionais sobre apenas no acesso de tempo, consulte [gerenciar o acesso de máquina virtual usando no momento.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span><span class="sxs-lookup"><span data-stu-id="8054f-159">For instructions on how toodo this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="8054f-160">Como fazer para implementar as recomendações de segurança do ASC?</span><span class="sxs-lookup"><span data-stu-id="8054f-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="8054f-161">Quando a Central de Segurança identifica possíveis vulnerabilidades de segurança, cria recomendações.</span><span class="sxs-lookup"><span data-stu-id="8054f-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="8054f-162">recomendações de saudação orientará você durante processo de saudação do configurando controles de saudação necessário.</span><span class="sxs-lookup"><span data-stu-id="8054f-162">hello recommendations guide you through hello process of configuring hello needed controls.</span></span> 
1. <span data-ttu-id="8054f-163">Selecione Olá **recomendações** bloco no painel ASC hello.</span><span class="sxs-lookup"><span data-stu-id="8054f-163">Select hello **Recommendations** tile on hello ASC dashboard.</span></span>

2. <span data-ttu-id="8054f-164">Exibir recomendações de saudação, que são mostradas em um formato de tabela em que cada linha representa uma recomendação.</span><span class="sxs-lookup"><span data-stu-id="8054f-164">View hello recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="8054f-165">recomendações de toofilter, selecione **filtro** e selecione os valores de severidade e estado de saudação desejar toosee.</span><span class="sxs-lookup"><span data-stu-id="8054f-165">toofilter recommendations, select **Filter** and select hello severity and state values you wish toosee.</span></span>

4. <span data-ttu-id="8054f-166">toodismiss uma recomendação não é aplicável, você pode clique com botão direito e selecione **ignorar.**</span><span class="sxs-lookup"><span data-stu-id="8054f-166">toodismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="8054f-167">Avalie qual recomendação deve ser aplicada primeiro.</span><span class="sxs-lookup"><span data-stu-id="8054f-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="8054f-168">Aplica recomendações de saudação em ordem de prioridade.</span><span class="sxs-lookup"><span data-stu-id="8054f-168">Apply hello recommendations in order of priority.</span></span>

<span data-ttu-id="8054f-169">Para obter uma lista de recomendações possíveis e instruções passo a passo sobre como tooapply cada, consulte [Gerenciando recomendações de segurança na Central de segurança do Azure.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span><span class="sxs-lookup"><span data-stu-id="8054f-169">For a list of possible recommendations and walk-throughs on how tooapply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="8054f-170">Detecção e resposta</span><span class="sxs-lookup"><span data-stu-id="8054f-170">Detection and Response</span></span>

<span data-ttu-id="8054f-171">Detecção e resposta vá juntas, conforme desejar toorespond assim que possível após uma ameaça é detectada.</span><span class="sxs-lookup"><span data-stu-id="8054f-171">Detection and response go together, as you want toorespond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="8054f-172">A detecção de ameaças ASC funciona automaticamente Coletando informações de segurança de seus recursos do Azure, rede hello e soluções de parceiros conectado.</span><span class="sxs-lookup"><span data-stu-id="8054f-172">ASC threat detection works by automatically collecting security information from your Azure resources, hello network, and connected partner solutions.</span></span> <span data-ttu-id="8054f-173">O ASC pode atualizar rapidamente seus algoritmos de detecção conforme os invasores lançam explorações novas e cada vez mais sofisticadas.</span><span class="sxs-lookup"><span data-stu-id="8054f-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="8054f-174">Para obter informações mais detalhadas sobre como funciona a detecção de ameaças do ASC, consulte [Funcionalidades de detecção da Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span><span class="sxs-lookup"><span data-stu-id="8054f-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a><span data-ttu-id="8054f-175">Como gerenciar e responder a alertas toosecurity?</span><span class="sxs-lookup"><span data-stu-id="8054f-175">How do I manage and respond toosecurity alerts?</span></span>

<span data-ttu-id="8054f-176">É mostrada uma lista de alertas de segurança priorizados na Central de segurança junto com hello informações que você precisa tooquickly investigar o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="8054f-176">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem.</span></span> <span data-ttu-id="8054f-177">Central de segurança também inclui recomendações sobre como tooremediate um ataque.</span><span class="sxs-lookup"><span data-stu-id="8054f-177">Security Center also includes recommendations for how tooremediate an attack.</span></span> <span data-ttu-id="8054f-178">toomanage a segurança de alertas, fazer Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="8054f-178">toomanage your security alerts, do hello following:</span></span>

1. <span data-ttu-id="8054f-179">Selecione Olá **alertas de segurança** bloco no painel de controle do hello ASC.</span><span class="sxs-lookup"><span data-stu-id="8054f-179">Select hello **Security alerts** tile in hello ASC dashboard.</span></span> <span data-ttu-id="8054f-180">Isso mostra detalhes de cada alerta.</span><span class="sxs-lookup"><span data-stu-id="8054f-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="8054f-181">Selecione toofilter alertas com base na data, estado e gravidade, **filtro** e selecione os valores hello deseja toosee.</span><span class="sxs-lookup"><span data-stu-id="8054f-181">toofilter alerts based on date, state, and severity, select **Filter** and then select hello values you want toosee.</span></span>

3. <span data-ttu-id="8054f-182">toorespond tooan alerta, selecioná-la e examinar as informações de saudação, selecione Olá recurso que foi atacado.</span><span class="sxs-lookup"><span data-stu-id="8054f-182">toorespond tooan alert, select it and review hello information, then select hello resource that was attacked.</span></span>

4. <span data-ttu-id="8054f-183">Em Olá **descrição** campo, você verá os detalhes, incluindo correção recomendada.</span><span class="sxs-lookup"><span data-stu-id="8054f-183">In hello **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="8054f-184">Para obter mais instruções sobre alertas de toosecurity está respondendo, consulte [toosecurity está respondendo e gerenciamento de alertas na Central de segurança do Azure.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span><span class="sxs-lookup"><span data-stu-id="8054f-184">For more detailed instructions on responding toosecurity alerts, see [Managing and responding toosecurity alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="8054f-185">Para obter ajuda na investigação de alertas de segurança, a empresa Olá pode integrar alertas ASC com sua própria solução SIEM, usando [integração do Azure Log](https://aka.ms/AzLog).</span><span class="sxs-lookup"><span data-stu-id="8054f-185">For further help in investigating security alerts, hello company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="8054f-186">Como fazer para gerenciar incidentes de segurança?</span><span class="sxs-lookup"><span data-stu-id="8054f-186">How do I manage security incidents?</span></span>

<span data-ttu-id="8054f-187">No ASC, um incidente de segurança é uma agregação de todos os alertas de um recurso que se alinham com os padrões da cadeia de encerramento.</span><span class="sxs-lookup"><span data-stu-id="8054f-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="8054f-188">Um incidente revelará a lista de saudação de alertas relacionados, que permite que você tooobtain obter mais informações sobre cada ocorrência.</span><span class="sxs-lookup"><span data-stu-id="8054f-188">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span> <span data-ttu-id="8054f-189">Incidentes aparecem na hello bloco alertas de segurança e de folha.</span><span class="sxs-lookup"><span data-stu-id="8054f-189">Incidents appear in hello Security Alerts tile and blade.</span></span>

<span data-ttu-id="8054f-190">tooreview e gerenciar incidentes de segurança, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="8054f-190">tooreview and manage security incidents, do hello following:</span></span>

1. <span data-ttu-id="8054f-191">Selecione Olá **alertas de segurança** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="8054f-191">Select hello **Security alerts** tile.</span></span> <span data-ttu-id="8054f-192">Se for detectado um incidente de segurança, ele será exibido no gráfico de alertas de segurança hello.</span><span class="sxs-lookup"><span data-stu-id="8054f-192">if a security incident is detected, it will appear under hello security alerts graph.</span></span> <span data-ttu-id="8054f-193">Ele terá um ícone diferente dos outros alertas.</span><span class="sxs-lookup"><span data-stu-id="8054f-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="8054f-194">Selecione toosee incidente hello mais detalhes sobre este incidente de segurança.</span><span class="sxs-lookup"><span data-stu-id="8054f-194">Select hello incident toosee more details about this security incident.</span></span> <span data-ttu-id="8054f-195">Detalhes adicionais incluem sua descrição completa, sua severidade, seu estado atual, Olá atacado recursos, etapas de correção de saudação incidente hello e Olá alertas que foram incluídos neste incidente.</span><span class="sxs-lookup"><span data-stu-id="8054f-195">Additional details include its full description, its severity, its current state, hello attacked resource, hello remediation steps for hello incident, and hello alerts that were included in this incident.</span></span>

<span data-ttu-id="8054f-196">Você pode filtrar toosee **incidentes apenas**, **alertas somente**, ou **ambos**.</span><span class="sxs-lookup"><span data-stu-id="8054f-196">You can filter toosee **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a><span data-ttu-id="8054f-197">Como acessar o relatório de inteligência de ameaça de Olá?</span><span class="sxs-lookup"><span data-stu-id="8054f-197">How do I access hello Threat Intelligence Report?</span></span>

<span data-ttu-id="8054f-198">ASC analisa informações contra ameaças de tooidentify várias fontes.</span><span class="sxs-lookup"><span data-stu-id="8054f-198">ASC analyzes information from multiple sources tooidentify threats.</span></span> <span data-ttu-id="8054f-199">as equipes de resposta a incidentes tooassist investigam e corrigir ameaças, Central de segurança inclui um relatório de inteligência de ameaça que contém informações sobre a ameaça de saudação que foi detectada.</span><span class="sxs-lookup"><span data-stu-id="8054f-199">tooassist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about hello threat that was detected.</span></span>

<span data-ttu-id="8054f-200">A Central de Segurança tem três tipos de relatórios de ameaça, que podem variar de acordo com o ataque.</span><span class="sxs-lookup"><span data-stu-id="8054f-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="8054f-201">Olá relatórios disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="8054f-201">hello reports available are:</span></span>

- <span data-ttu-id="8054f-202">Relatório de Grupo de Atividade: fornece análises avançadas sobre os invasores, seus objetivos e táticas.</span><span class="sxs-lookup"><span data-stu-id="8054f-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="8054f-203">Relatório de Campanha: concentra-se nos detalhes de campanhas de ataque específicas.</span><span class="sxs-lookup"><span data-stu-id="8054f-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="8054f-204">Relatório de resumo de ameaça: abrange todos os itens em dois relatórios de saudação anterior.</span><span class="sxs-lookup"><span data-stu-id="8054f-204">Threat Summary Report: covers all items in hello previous two reports.</span></span>

<span data-ttu-id="8054f-205">Esse tipo de informação é muito útil durante o processo de resposta a incidentes hello, onde houver uma fonte de saudação toounderstand investigação em andamento de ataque hello, Olá motivações do invasor e quais toomitigate toodo esse problema futuramente.</span><span class="sxs-lookup"><span data-stu-id="8054f-205">This type of information is very useful during hello incident response process, where there is an ongoing investigation toounderstand hello source of hello attack, hello attacker’s motivations, and what toodo toomitigate this issue moving forward.</span></span>

1. <span data-ttu-id="8054f-206">tooaccess Olá inteligência de ameaça de relatório, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="8054f-206">tooaccess hello threat intelligence report, do hello following:</span></span>

2. <span data-ttu-id="8054f-207">Selecione Olá **alertas de segurança** bloco no painel ASC hello.</span><span class="sxs-lookup"><span data-stu-id="8054f-207">Select hello **Security alerts** tile on hello ASC dashboard.</span></span>

3. <span data-ttu-id="8054f-208">Selecione o alerta de segurança de saudação do qual você deseja tooobtain obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="8054f-208">Select hello security alert for which you want tooobtain more information.</span></span>

4. <span data-ttu-id="8054f-209">Em Olá **relatórios** , clique em relatório de inteligência de ameaça Olá link toohello.</span><span class="sxs-lookup"><span data-stu-id="8054f-209">In hello **Reports** field, click hello link toohello threat intelligence report.</span></span>

5. <span data-ttu-id="8054f-210">Isso abrirá o arquivo PDF hello, o que pode ser baixado.</span><span class="sxs-lookup"><span data-stu-id="8054f-210">This will open hello PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="8054f-211">Para obter informações adicionais sobre Olá relatório de inteligência de ameaça ASC, consulte [o relatório de inteligência de ameaça do Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="8054f-211">For additional information about hello ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="8054f-212">Avaliação</span><span class="sxs-lookup"><span data-stu-id="8054f-212">Assessment</span></span>

<span data-ttu-id="8054f-213">toohelp com avaliação, teste e avaliação de sua postura de segurança, ASC fornece para avaliação de vulnerabilidade integrado com Qualys agentes de nuvem, como parte de seu componente de recomendações de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8054f-213">toohelp with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="8054f-214">Olá Qualys agente relatórios vulnerabilidade dados toohello Qualys plataforma de gerenciamento, que envia dados de monitoramento de integridade e vulnerabilidade fazer tooASC.</span><span class="sxs-lookup"><span data-stu-id="8054f-214">hello Qualys agent reports vulnerability data toohello Qualys management platform, which then sends vulnerability and health monitoring data back tooASC.</span></span> <span data-ttu-id="8054f-215">Olá recomendação tooadd uma solução de avaliação de vulnerabilidade é exibida no hello **recomendações** folha no painel de controle do hello ASC.</span><span class="sxs-lookup"><span data-stu-id="8054f-215">hello recommendation tooadd a vulnerability assessment solution is displayed in hello **Recommendations** blade on hello ASC dashboard.</span></span>

<span data-ttu-id="8054f-216">Após a solução de avaliação de vulnerabilidade hello está instalada na VM de destino Olá, verificações de segurança central Olá toodetect VM e identificam vulnerabilidades do sistema e do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8054f-216">After hello vulnerability assessment solution is installed on hello target VM, Security Center scans hello VM toodetect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="8054f-217">Detectados problemas são mostrados em Olá **recomendações de máquinas virtuais** opção.</span><span class="sxs-lookup"><span data-stu-id="8054f-217">Detected issues are shown under hello **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="8054f-218">Como fazer para implementar uma solução de avaliação de vulnerabilidade?</span><span class="sxs-lookup"><span data-stu-id="8054f-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="8054f-219">Se uma Máquina Virtual não tem uma solução de avaliação de vulnerabilidade integrada já implantada, a Central de Segurança recomenda que ela seja instalada.</span><span class="sxs-lookup"><span data-stu-id="8054f-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="8054f-220">No painel ASC hello, em Olá **recomendações** folha, selecione **adicionar uma solução de avaliação de vulnerabilidade.**</span><span class="sxs-lookup"><span data-stu-id="8054f-220">In hello ASC dashboard, on hello **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="8054f-221">Selecione VMs Olá onde deseja que a solução de avaliação de vulnerabilidade tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="8054f-221">Select hello VMs where you want tooinstall hello vulnerability assessment solution.</span></span>

3. <span data-ttu-id="8054f-222">Clique em **Instalar em [número de] VMs.**</span><span class="sxs-lookup"><span data-stu-id="8054f-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="8054f-223">Selecione uma solução de parceiro no hello Azure Marketplace ou em **usar solução existente,** selecione **Qualys.**</span><span class="sxs-lookup"><span data-stu-id="8054f-223">Select a partner solution in hello Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="8054f-224">Você pode ativar as configurações de atualização do hello automática ou desativar Olá **soluções de parceiros** folha.</span><span class="sxs-lookup"><span data-stu-id="8054f-224">You can turn hello auto update settings on or off in hello **Partner Solutions** blade.</span></span>

<span data-ttu-id="8054f-225">Para obter mais instruções sobre como tooimplement uma solução de avaliação de vulnerabilidade, consulte [avaliação de vulnerabilidade na Central de segurança do Azure.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span><span class="sxs-lookup"><span data-stu-id="8054f-225">For further instructions on how tooimplement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8054f-226">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8054f-226">Next steps</span></span>

- [<span data-ttu-id="8054f-227">Guia de início rápido da Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="8054f-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="8054f-228">Introdução tooAzure Central de segurança</span><span class="sxs-lookup"><span data-stu-id="8054f-228">Introduction tooAzure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="8054f-229">Integrando alertas da Central de Segurança do Azure com a integração de logs do Azure</span><span class="sxs-lookup"><span data-stu-id="8054f-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [<span data-ttu-id="8054f-230">Melhorar a Central de Segurança do Azure com a avaliação de vulnerabilidade integrada</span><span class="sxs-lookup"><span data-stu-id="8054f-230">Boost Azure Security Center with Integrated Vulnerability Assessment</span></span>](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
