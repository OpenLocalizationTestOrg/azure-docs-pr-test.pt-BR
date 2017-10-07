---
title: "taxa de transferência de rede de VM do Azure aaaTesting | Microsoft Docs"
description: "Saiba como taxa de transferência da rede tootest máquina virtual do Azure."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="0188a-103">Teste de Largura de Banda/Taxa de Transferência (NTTTCP)</span><span class="sxs-lookup"><span data-stu-id="0188a-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="0188a-104">Ao testar o desempenho de taxa de transferência de rede no Azure, é melhor toouse uma ferramenta que tem como alvo a rede Olá para teste e minimiza o uso de saudação de outros recursos que podem afetar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="0188a-104">When testing network throughput performance in Azure, it's best toouse a tool that targets hello network for testing and minimizes hello use of other resources that could impact performance.</span></span> <span data-ttu-id="0188a-105">É recomendável usar o NTTTCP.</span><span class="sxs-lookup"><span data-stu-id="0188a-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="0188a-106">Copiar Olá ferramenta tootwo VMs do Azure de saudação mesmo tamanho.</span><span class="sxs-lookup"><span data-stu-id="0188a-106">Copy hello tool tootwo Azure VMs of hello same size.</span></span> <span data-ttu-id="0188a-107">Uma máquina virtual funciona como remetente e hello como destinatário.</span><span class="sxs-lookup"><span data-stu-id="0188a-107">One VM functions as SENDER and hello other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="0188a-108">Implantando VMs para teste</span><span class="sxs-lookup"><span data-stu-id="0188a-108">Deploying VMs for testing</span></span>
<span data-ttu-id="0188a-109">Para fins de saudação desse teste, Olá duas VMs devem estar no Olá mesmo serviço de nuvem ou Olá mesmo conjunto de disponibilidade para que possamos pode usar os IPs internos e excluir Olá balanceadores de carga de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="0188a-109">For hello purposes of this test, hello two VMs should be in either hello same Cloud Service or hello same Availability Set so that we can use their internal IPs and exclude hello Load Balancers from hello test.</span></span> <span data-ttu-id="0188a-110">É possível tootest com hello VIP, mas esse tipo de teste está fora do escopo deste documento hello.</span><span class="sxs-lookup"><span data-stu-id="0188a-110">It is possible tootest with hello VIP but this kind of testing is outside hello scope of this document.</span></span>
 
<span data-ttu-id="0188a-111">Tome nota do endereço IP do destinatário hello.</span><span class="sxs-lookup"><span data-stu-id="0188a-111">Make a note of hello RECEIVER's IP address.</span></span> <span data-ttu-id="0188a-112">Vamos chamar esse IP de “a.b.c.r”</span><span class="sxs-lookup"><span data-stu-id="0188a-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="0188a-113">Anote Olá número de núcleos na VM de saudação.</span><span class="sxs-lookup"><span data-stu-id="0188a-113">Make a note of hello number of cores on hello VM.</span></span> <span data-ttu-id="0188a-114">Vamos chamar isso de “\#num\_cores”</span><span class="sxs-lookup"><span data-stu-id="0188a-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="0188a-115">Execute Olá NTTTCP de teste para 300 segundos (ou 5 minutos) no remetente Olá VM e o destinatário VM.</span><span class="sxs-lookup"><span data-stu-id="0188a-115">Run hello NTTTCP test for 300 seconds (or 5 minutes) on hello sender VM and receiver VM.</span></span>

<span data-ttu-id="0188a-116">Dica: Ao configurar este teste para Olá primeira vez, você pode tentar um comentário de tooget período mais curto do teste mais cedo.</span><span class="sxs-lookup"><span data-stu-id="0188a-116">Tip: When setting up this test for hello first time, you might try a shorter test period tooget feedback sooner.</span></span> <span data-ttu-id="0188a-117">Depois que a ferramenta hello está funcionando conforme o esperado, estenda segundos de too300 período de teste Olá para obter resultados mais precisos hello.</span><span class="sxs-lookup"><span data-stu-id="0188a-117">Once hello tool is working as expected, extend hello test period too300 seconds for hello most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="0188a-118">remetente Olá **e** receptor deve especificar **Olá mesmo** parâmetro de duração de teste (-t).</span><span class="sxs-lookup"><span data-stu-id="0188a-118">hello sender **and** receiver must specify **hello same** test duration parameter (-t).</span></span>

<span data-ttu-id="0188a-119">tootest um único fluxo TCP 10 segundos:</span><span class="sxs-lookup"><span data-stu-id="0188a-119">tootest a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="0188a-120">Parâmetros do receptor: ntttcp -r -t 10 -P 1</span><span class="sxs-lookup"><span data-stu-id="0188a-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="0188a-121">Parâmetros do remetente: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="0188a-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="0188a-122">Olá anterior exemplo só deve ser usado tooconfirm sua configuração.</span><span class="sxs-lookup"><span data-stu-id="0188a-122">hello preceding sample should only be used tooconfirm your configuration.</span></span> <span data-ttu-id="0188a-123">Exemplos válidos de teste são abordados adiante neste documento.</span><span class="sxs-lookup"><span data-stu-id="0188a-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="0188a-124">Testando VMs que executam o WINDOWS:</span><span class="sxs-lookup"><span data-stu-id="0188a-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-hello-vms"></a><span data-ttu-id="0188a-125">Obter NTTTCP para Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="0188a-125">Get NTTTCP onto hello VMs.</span></span>

<span data-ttu-id="0188a-126">Baixar a versão mais recente do hello: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="0188a-126">Download hello latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="0188a-127">Se preferir, pesquise-a, caso tenha sido movida: <https://www.bing.com/search?q=ntttcp+download>\< – deve ser a primeira ocorrência</span><span class="sxs-lookup"><span data-stu-id="0188a-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="0188a-128">Considere colocar o NTTTCP em uma pasta separada, como c:\\tools</span><span class="sxs-lookup"><span data-stu-id="0188a-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a><span data-ttu-id="0188a-129">Permitir NTTTCP através do firewall do Windows hello</span><span class="sxs-lookup"><span data-stu-id="0188a-129">Allow NTTTCP through hello Windows firewall</span></span>
<span data-ttu-id="0188a-130">No hello RECEPTOR, crie uma regra de permissão tooallow do Firewall do Windows hello tooarrive de tráfego de NTTTCP.</span><span class="sxs-lookup"><span data-stu-id="0188a-130">On hello RECEIVER, create an Allow rule on hello Windows Firewall tooallow the NTTTCP traffic tooarrive.</span></span> <span data-ttu-id="0188a-131">É mais fácil tooallow Olá NTTTCP programa inteiro por nome em vez de tooallow portas TCP de entrada.</span><span class="sxs-lookup"><span data-stu-id="0188a-131">It's easiest tooallow hello entire NTTTCP program by name rather than tooallow specific TCP ports inbound.</span></span>

<span data-ttu-id="0188a-132">Permitir ntttcp por meio de saudação Firewall do Windows como este:</span><span class="sxs-lookup"><span data-stu-id="0188a-132">Allow ntttcp through hello Windows Firewall like this:</span></span>

<span data-ttu-id="0188a-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="0188a-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="0188a-134">Por exemplo, se você copiou ntttcp.exe toohello "c:\\ferramentas" pasta, isso seria comando hello:</span><span class="sxs-lookup"><span data-stu-id="0188a-134">For example, if you copied ntttcp.exe toohello "c:\\tools" folder, this would be hello command:</span></span> 

<span data-ttu-id="0188a-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="0188a-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="0188a-136">Executando testes NTTTCP</span><span class="sxs-lookup"><span data-stu-id="0188a-136">Running NTTTCP tests</span></span>

<span data-ttu-id="0188a-137">Iniciar NTTTCP em Olá RECEPTOR (**executar de CMD**, não do PowerShell):</span><span class="sxs-lookup"><span data-stu-id="0188a-137">Start NTTTCP on hello RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="0188a-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span><span class="sxs-lookup"><span data-stu-id="0188a-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="0188a-139">Se Olá VM tem quatro núcleos e um endereço IP de 10.0.0.4, ele teria esta aparência:</span><span class="sxs-lookup"><span data-stu-id="0188a-139">If hello VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="0188a-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="0188a-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="0188a-141">Iniciar NTTTCP em Olá remetente (**executar de CMD**, não do PowerShell):</span><span class="sxs-lookup"><span data-stu-id="0188a-141">Start NTTTCP on hello SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="0188a-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="0188a-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="0188a-143">Aguarde até que os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="0188a-143">Wait for hello results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="0188a-144">Testando VMs que executam o LINUX:</span><span class="sxs-lookup"><span data-stu-id="0188a-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="0188a-145">Use nttcp-for-linux.</span><span class="sxs-lookup"><span data-stu-id="0188a-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="0188a-146">Ele está disponível em <https://github.com/Microsoft/ntttcp-for-linux></span><span class="sxs-lookup"><span data-stu-id="0188a-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="0188a-147">No hello VMs do Linux (remetente e destinatário), execute estes comandos para preparar ntttcp para linux em suas VMs:</span><span class="sxs-lookup"><span data-stu-id="0188a-147">On hello Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="0188a-148">CentOS – Instalar o Git:</span><span class="sxs-lookup"><span data-stu-id="0188a-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="0188a-149">Ubuntu – Instalar o Git:</span><span class="sxs-lookup"><span data-stu-id="0188a-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="0188a-150">Crie e instale nas duas:</span><span class="sxs-lookup"><span data-stu-id="0188a-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="0188a-151">Como exemplo do Windows hello, vamos supor que IP do RECEPTOR de Linux Olá será 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="0188a-151">As in hello Windows example, we assume hello Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="0188a-152">Inicie NTTTCP para Linux em Olá destinatário:</span><span class="sxs-lookup"><span data-stu-id="0188a-152">Start NTTTCP-for-Linux on hello RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="0188a-153">E em Olá remetente, execute:</span><span class="sxs-lookup"><span data-stu-id="0188a-153">And on hello SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="0188a-154">Teste comprimento padrão é too60 segundos se nenhum parâmetro de tempo é fornecido</span><span class="sxs-lookup"><span data-stu-id="0188a-154">Test length defaults too60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="0188a-155">Testar entre VMs executando o Windows e LINUX:</span><span class="sxs-lookup"><span data-stu-id="0188a-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="0188a-156">Este cenários é deve habilitar o modo de sincronização não Olá para que teste Olá possa ser executados.</span><span class="sxs-lookup"><span data-stu-id="0188a-156">On this scenarios we should enable hello no-sync mode so hello test can run.</span></span> <span data-ttu-id="0188a-157">Isso é feito usando Olá **sinalizador -N** para Linux e **sinalizador -ns** para Windows.</span><span class="sxs-lookup"><span data-stu-id="0188a-157">This is done by using hello **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-toowindows"></a><span data-ttu-id="0188a-158">De tooWindows Linux:</span><span class="sxs-lookup"><span data-stu-id="0188a-158">From Linux tooWindows:</span></span>

<span data-ttu-id="0188a-159">Receptor <Windows>:</span><span class="sxs-lookup"><span data-stu-id="0188a-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="0188a-160">Remetente <Linux> :</span><span class="sxs-lookup"><span data-stu-id="0188a-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a><span data-ttu-id="0188a-161">Do Windows tooLinux:</span><span class="sxs-lookup"><span data-stu-id="0188a-161">From Windows tooLinux:</span></span>

<span data-ttu-id="0188a-162">Receptor <Linux>:</span><span class="sxs-lookup"><span data-stu-id="0188a-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="0188a-163">Remetente <Windows>:</span><span class="sxs-lookup"><span data-stu-id="0188a-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="0188a-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0188a-164">Next steps</span></span>
* <span data-ttu-id="0188a-165">Dependendo de resultados, pode haver espaço muito[otimizar máquinas de taxa de transferência de rede](virtual-network-optimize-network-bandwidth.md) para seu cenário.</span><span class="sxs-lookup"><span data-stu-id="0188a-165">Depending on results, there may be room too[Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="0188a-166">Saiba mais com as [Perguntas frequentes sobre a Rede Virtual do Azure](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="0188a-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
