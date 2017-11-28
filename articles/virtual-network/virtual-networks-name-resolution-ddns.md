---
title: "Usando o DNS Dinâmico para registrar nomes de host"
description: "Esta página fornece detalhes sobre como configurar o DNS dinâmico para registrar os nomes de host em seus próprios servidores DNS."
services: dns
documentationcenter: na
author: GarethBradshawMSFT
manager: timlt
editor: 
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: garbrad
ms.openlocfilehash: 440a062e5fff73526b2d77d7d0a7c52ca72a66f1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-dynamic-dns-to-register-hostnames-in-your-own-dns-server"></a><span data-ttu-id="51371-103">Usando o DNS dinâmico para registrar os nomes de host em seu próprio servidor DNS</span><span class="sxs-lookup"><span data-stu-id="51371-103">Using Dynamic DNS to register hostnames in your own DNS server</span></span>
<span data-ttu-id="51371-104">[Azure fornece resolução de nomes](virtual-networks-name-resolution-for-vms-and-role-instances.md) para VMs (máquinas virtuais) e instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="51371-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="51371-105">Contudo, quando a resolução de nome precisar ir além do que é fornecido pelo Azure, você pode fornecer seus próprios servidores DNS.</span><span class="sxs-lookup"><span data-stu-id="51371-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="51371-106">Isso permite que você personalize sua solução DNS para ajustá-la às suas próprias necessidades específicas.</span><span class="sxs-lookup"><span data-stu-id="51371-106">This gives you the power to tailor your DNS solution to suit your own specific needs.</span></span> <span data-ttu-id="51371-107">Por exemplo, você poderá precisar acessar recursos locais por meio do controlador de domínio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="51371-107">For example, you may need to access on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="51371-108">Quando os servidores DNS personalizados forem hospedados como VMs do Azure, você poderá encaminhar consultas de nome de host para a mesma rede virtual do Azure para resolver nomes de host.</span><span class="sxs-lookup"><span data-stu-id="51371-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for the same vnet to Azure to resolve hostnames.</span></span> <span data-ttu-id="51371-109">Se você não desejar usar essa rota, você poderá registrar os nomes de host da VM no servidor DNS usando o DNS Dinâmico.</span><span class="sxs-lookup"><span data-stu-id="51371-109">If you do not wish to use this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="51371-110">O Azure não tem a capacidade (por exemplo, credenciais) para criar diretamente registros nos servidores DNS, de modo que organizações alternativas são muitas vezes necessárias.</span><span class="sxs-lookup"><span data-stu-id="51371-110">Azure doesn't have the ability (e.g. credentials) to directly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="51371-111">Aqui estão alguns cenários comuns com alternativas.</span><span class="sxs-lookup"><span data-stu-id="51371-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="51371-112">Clientes do Windows</span><span class="sxs-lookup"><span data-stu-id="51371-112">Windows clients</span></span>
<span data-ttu-id="51371-113">Clientes do Windows não unidos por domínio tentam atualizações não seguras de DNS dinâmico (DDNS) quando eles são inicializados ou quando seu endereço IP for alterado.</span><span class="sxs-lookup"><span data-stu-id="51371-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="51371-114">O nome DNS é o nome do host mais o sufixo DNS primário.</span><span class="sxs-lookup"><span data-stu-id="51371-114">The DNS name is the hostname plus the primary DNS suffix.</span></span> <span data-ttu-id="51371-115">O Azure deixa o sufixo DNS primário em branco, mas você pode configurá-lo na VM, por meio da [interface do usuário](https://technet.microsoft.com/library/cc794784.aspx) ou [usando a automação](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span><span class="sxs-lookup"><span data-stu-id="51371-115">Azure leaves the primary DNS suffix blank, but you can set this in the VM, via the [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="51371-116">Os clientes unidos por domínio do Windows registram seus endereços IP com o controlador de domínio usando o DNS dinâmico seguro.</span><span class="sxs-lookup"><span data-stu-id="51371-116">Domain-joined Windows clients register their IP addresses with the domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="51371-117">O processo de ingresso no domínio define o sufixo DNS primário no cliente e cria e mantém a relação de confiança.</span><span class="sxs-lookup"><span data-stu-id="51371-117">The domain-join process sets the primary DNS suffix on the client and creates and maintains the trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="51371-118">Clientes Linux</span><span class="sxs-lookup"><span data-stu-id="51371-118">Linux clients</span></span>
<span data-ttu-id="51371-119">Clientes Linux geralmente não se registram no servidor DNS na inicialização, eles supõem que o servidor DHCP faça isso.</span><span class="sxs-lookup"><span data-stu-id="51371-119">Linux clients generally don't register themselves with the DNS server on startup, they assume the DHCP server does it.</span></span> <span data-ttu-id="51371-120">Os servidores DHCP do Azure não são capazes ou não tem as credenciais para manter os registros no seu servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="51371-120">Azure's DHCP servers do not have the ability or credentials to register records in your DNS server.</span></span>  <span data-ttu-id="51371-121">Você pode usar uma ferramenta chamada *nsupdate*, que está incluída no pacote de Associação, para enviar atualizações do DNS dinâmico.</span><span class="sxs-lookup"><span data-stu-id="51371-121">You can use a tool called *nsupdate*, which is included in the Bind package, to send Dynamic DNS updates.</span></span> <span data-ttu-id="51371-122">Como o protocolo DNS dinâmico é padronizado, você pode usar *nsupdate* mesmo quando não estiver usando Associação no servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="51371-122">Because the Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on the DNS server.</span></span>

<span data-ttu-id="51371-123">Você pode usar os ganchos que são fornecidos pelo cliente DHCP para criar e manter a entrada do nome do host no servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="51371-123">You can use the hooks that are provided by the DHCP client to create and maintain the hostname entry in the DNS server.</span></span> <span data-ttu-id="51371-124">Durante o ciclo DHCP, o cliente executa os scripts em */etc/dhcp/dhclient-exit-hooks.d/*.</span><span class="sxs-lookup"><span data-stu-id="51371-124">During the DHCP cycle, the client executes the scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="51371-125">Isso pode ser usado para registrar o novo endereço IP usando *nsupdate*.</span><span class="sxs-lookup"><span data-stu-id="51371-125">This can be used to register the new IP address by using *nsupdate*.</span></span> <span data-ttu-id="51371-126">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="51371-126">For example:</span></span>

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on the primary nic
        if [ "$interface" != "eth0" ]
        then
            return
        fi

        # when we have a new IP, perform nsupdate
        if [ "$reason" = BOUND ] || [ "$reason" = RENEW ] ||
           [ "$reason" = REBIND ] || [ "$reason" = REBOOT ]
        then
            host=`hostname`
            nsupdatecmds=/var/tmp/nsupdatecmds
              echo "update delete $host.$requireddomain a" > $nsupdatecmds
              echo "update add $host.$requireddomain 3600 a $new_ip_address" >> $nsupdatecmds
              echo "send" >> $nsupdatecmds

              nsupdate $nsupdatecmds
        fi

        
        

<span data-ttu-id="51371-127">Você também pode usar o comando *nsupdate* para executar atualizações DNS Dinâmicas.</span><span class="sxs-lookup"><span data-stu-id="51371-127">You can also use the *nsupdate* command to perform secure Dynamic DNS updates.</span></span> <span data-ttu-id="51371-128">Por exemplo, quando você estiver usando um servidor DNS de associação, um par de chaves públicas-privadas será [gerado](http://linux.yyz.us/nsupdate/).</span><span class="sxs-lookup"><span data-stu-id="51371-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="51371-129">O servidor DNS é [configurado](http://linux.yyz.us/dns/ddns-server.html) com a parte pública da chave para que ele possa verificar a assinatura da solicitação.</span><span class="sxs-lookup"><span data-stu-id="51371-129">The DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with the public part of the key so that it can verify the signature on the request.</span></span> <span data-ttu-id="51371-130">Você deve usar a opção *-k* para fornecer o par de chaves para *nsupdate* para que o DNS dinâmico atualize a solicitação a ser assinada.</span><span class="sxs-lookup"><span data-stu-id="51371-130">You must use the *-k* option to provide the key-pair to *nsupdate* in order for the Dynamic DNS update request to be signed.</span></span>

<span data-ttu-id="51371-131">Quando estiver usando um servidor DNS do Windows, você poderá usar a autenticação Kerberos com o parâmetro *-g* em *nsupdate* (não está disponível na versão do Windows *nsupdate*).</span><span class="sxs-lookup"><span data-stu-id="51371-131">When you're using a Windows DNS server, you can use Kerberos authentication with the *-g* parameter in *nsupdate* (not available in the Windows version of *nsupdate*).</span></span> <span data-ttu-id="51371-132">Para fazer isso, use *kinit* para carregar as credenciais (por exemplo, um [arquivo keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span><span class="sxs-lookup"><span data-stu-id="51371-132">To do this, use *kinit* to load the credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="51371-133">Em seguida, *nsupdate -g* selecionará as credenciais do cache.</span><span class="sxs-lookup"><span data-stu-id="51371-133">Then *nsupdate -g* will pick up the credentials from the cache.</span></span>

<span data-ttu-id="51371-134">Se necessário, você pode adicionar um sufixo de pesquisa DNS em suas VMs.</span><span class="sxs-lookup"><span data-stu-id="51371-134">If needed, you can add a DNS search suffix to your VMs.</span></span> <span data-ttu-id="51371-135">O sufixo DNS é especificado no arquivo */etc/resolv.conf* .</span><span class="sxs-lookup"><span data-stu-id="51371-135">The DNS suffix is specified in the */etc/resolv.conf* file.</span></span> <span data-ttu-id="51371-136">A maioria das distribuições de Linux gerencia automaticamente o conteúdo desse arquivo, então, normalmente você não pode editá-lo.</span><span class="sxs-lookup"><span data-stu-id="51371-136">Most Linux distros automatically manage the content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="51371-137">No entanto, você pode substituir o sufixo, usando o comando *substituem* do cliente DHCP.</span><span class="sxs-lookup"><span data-stu-id="51371-137">However, you can override the suffix by using the DHCP client's *supersede* command.</span></span> <span data-ttu-id="51371-138">Para fazer isso, em */etc/dhcp/dhclient.conf*, adicione:</span><span class="sxs-lookup"><span data-stu-id="51371-138">To do this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

