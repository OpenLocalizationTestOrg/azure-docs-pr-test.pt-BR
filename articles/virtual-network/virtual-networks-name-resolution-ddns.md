---
title: "aaaUsing nomes de host DNS dinâmico tooregister"
description: "Esta página fornece detalhes sobre como tooset a nomes de host DNS dinâmico tooregister em seus próprios servidores DNS."
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
ms.openlocfilehash: 8d4b44265714e6976f26bfb3446e8101aa70996a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a><span data-ttu-id="8df20-103">Usando nomes de host DNS dinâmico tooregister em seu próprio servidor DNS</span><span class="sxs-lookup"><span data-stu-id="8df20-103">Using Dynamic DNS tooregister hostnames in your own DNS server</span></span>
<span data-ttu-id="8df20-104">[Azure fornece resolução de nomes](virtual-networks-name-resolution-for-vms-and-role-instances.md) para VMs (máquinas virtuais) e instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="8df20-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="8df20-105">Contudo, quando a resolução de nome precisar ir além do que é fornecido pelo Azure, você pode fornecer seus próprios servidores DNS.</span><span class="sxs-lookup"><span data-stu-id="8df20-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="8df20-106">Isso dá a você Olá power tootailor seu toosuit de solução DNS suas necessidades específicas.</span><span class="sxs-lookup"><span data-stu-id="8df20-106">This gives you hello power tootailor your DNS solution toosuit your own specific needs.</span></span> <span data-ttu-id="8df20-107">Por exemplo, talvez seja necessário tooaccess recursos de locais por meio do controlador de domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8df20-107">For example, you may need tooaccess on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="8df20-108">Quando seus servidores DNS personalizados são hospedados como máquinas virtuais do Azure que você pode encaminhar hostname consulta Olá mesmo vnet tooAzure tooresolve nomes de host.</span><span class="sxs-lookup"><span data-stu-id="8df20-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for hello same vnet tooAzure tooresolve hostnames.</span></span> <span data-ttu-id="8df20-109">Se você não desejar toouse essa rota, você pode registrar seu nome de host VM no seu servidor DNS usando DNS dinâmico.</span><span class="sxs-lookup"><span data-stu-id="8df20-109">If you do not wish toouse this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="8df20-110">Azure não tem Olá capacidade (por exemplo, credenciais) toodirectly criar registros em seus servidores DNS, para que organizações alternativas costumam ser necessárias.</span><span class="sxs-lookup"><span data-stu-id="8df20-110">Azure doesn't have hello ability (e.g. credentials) toodirectly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="8df20-111">Aqui estão alguns cenários comuns com alternativas.</span><span class="sxs-lookup"><span data-stu-id="8df20-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="8df20-112">Clientes do Windows</span><span class="sxs-lookup"><span data-stu-id="8df20-112">Windows clients</span></span>
<span data-ttu-id="8df20-113">Clientes do Windows não unidos por domínio tentam atualizações não seguras de DNS dinâmico (DDNS) quando eles são inicializados ou quando seu endereço IP for alterado.</span><span class="sxs-lookup"><span data-stu-id="8df20-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="8df20-114">nome DNS de saudação é hostname hello mais sufixo DNS primário de saudação.</span><span class="sxs-lookup"><span data-stu-id="8df20-114">hello DNS name is hello hostname plus hello primary DNS suffix.</span></span> <span data-ttu-id="8df20-115">Azure deixa o sufixo DNS primário de saudação em branco, mas você pode definir isso em Olá VM, por meio de saudação [UI](https://technet.microsoft.com/library/cc794784.aspx) ou [usando automação](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span><span class="sxs-lookup"><span data-stu-id="8df20-115">Azure leaves hello primary DNS suffix blank, but you can set this in hello VM, via hello [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="8df20-116">Clientes do Windows ingressado no domínio registrem seus endereços IP com o controlador de domínio hello usando DNS dinâmico seguro.</span><span class="sxs-lookup"><span data-stu-id="8df20-116">Domain-joined Windows clients register their IP addresses with hello domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="8df20-117">processo de associação de domínio Olá define o sufixo DNS primário Olá no cliente de saudação e cria e mantém a relação de confiança de saudação.</span><span class="sxs-lookup"><span data-stu-id="8df20-117">hello domain-join process sets hello primary DNS suffix on hello client and creates and maintains hello trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="8df20-118">Clientes Linux</span><span class="sxs-lookup"><span data-stu-id="8df20-118">Linux clients</span></span>
<span data-ttu-id="8df20-119">Os clientes do Linux geralmente não se registraram com o servidor DNS Olá na inicialização, ele assume um servidor DHCP de saudação faz isso.</span><span class="sxs-lookup"><span data-stu-id="8df20-119">Linux clients generally don't register themselves with hello DNS server on startup, they assume hello DHCP server does it.</span></span> <span data-ttu-id="8df20-120">Os servidores DHCP do Azure não tem capacidade de saudação ou registros de tooregister de credenciais no seu servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="8df20-120">Azure's DHCP servers do not have hello ability or credentials tooregister records in your DNS server.</span></span>  <span data-ttu-id="8df20-121">Você pode usar uma ferramenta chamada *nsupdate*, que está incluído no pacote de ligação hello, atualizações de DNS dinâmico toosend.</span><span class="sxs-lookup"><span data-stu-id="8df20-121">You can use a tool called *nsupdate*, which is included in hello Bind package, toosend Dynamic DNS updates.</span></span> <span data-ttu-id="8df20-122">Olá protocolo DNS dinâmico é padronizado, você pode usar *nsupdate* mesmo quando você não estiver usando Bind no servidor DNS hello.</span><span class="sxs-lookup"><span data-stu-id="8df20-122">Because hello Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on hello DNS server.</span></span>

<span data-ttu-id="8df20-123">Você pode usar ganchos de saudação que são fornecidos pelo toocreate de cliente DHCP hello e manter Olá entrada de nome de host do servidor DNS de saudação.</span><span class="sxs-lookup"><span data-stu-id="8df20-123">You can use hello hooks that are provided by hello DHCP client toocreate and maintain hello hostname entry in hello DNS server.</span></span> <span data-ttu-id="8df20-124">Durante o ciclo DHCP Olá, o cliente de saudação executa scripts Olá */etc/dhcp/dhclient-exit-hooks.d/*.</span><span class="sxs-lookup"><span data-stu-id="8df20-124">During hello DHCP cycle, hello client executes hello scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="8df20-125">Isso pode ser usado tooregister Olá novo endereço IP usando *nsupdate*.</span><span class="sxs-lookup"><span data-stu-id="8df20-125">This can be used tooregister hello new IP address by using *nsupdate*.</span></span> <span data-ttu-id="8df20-126">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8df20-126">For example:</span></span>

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on hello primary nic
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

        
        

<span data-ttu-id="8df20-127">Você também pode usar o hello *nsupdate* tooperform de comando de atualizações de DNS dinâmico seguro.</span><span class="sxs-lookup"><span data-stu-id="8df20-127">You can also use hello *nsupdate* command tooperform secure Dynamic DNS updates.</span></span> <span data-ttu-id="8df20-128">Por exemplo, quando você estiver usando um servidor DNS de associação, um par de chaves públicas-privadas será [gerado](http://linux.yyz.us/nsupdate/).</span><span class="sxs-lookup"><span data-stu-id="8df20-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="8df20-129">servidor de DNS Olá [configurado](http://linux.yyz.us/dns/ddns-server.html) com a parte pública de saudação da chave Olá para que ele possa verificar se a assinatura de saudação na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8df20-129">hello DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with hello public part of hello key so that it can verify hello signature on hello request.</span></span> <span data-ttu-id="8df20-130">Você deve usar o hello *-k* tooprovide opção Olá par de chaves muito*nsupdate* em ordem para Olá toobe solicitação assinado de atualização de DNS dinâmico.</span><span class="sxs-lookup"><span data-stu-id="8df20-130">You must use hello *-k* option tooprovide hello key-pair too*nsupdate* in order for hello Dynamic DNS update request toobe signed.</span></span>

<span data-ttu-id="8df20-131">Quando você estiver usando um servidor DNS do Windows, você pode usar a autenticação Kerberos com hello *-g* parâmetro em *nsupdate* (não disponível na versão do Windows de saudação *nsupdate* ).</span><span class="sxs-lookup"><span data-stu-id="8df20-131">When you're using a Windows DNS server, you can use Kerberos authentication with hello *-g* parameter in *nsupdate* (not available in hello Windows version of *nsupdate*).</span></span> <span data-ttu-id="8df20-132">toodo isso, use *kinit* credenciais de saudação tooload (por exemplo, de um [arquivo keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span><span class="sxs-lookup"><span data-stu-id="8df20-132">toodo this, use *kinit* tooload hello credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="8df20-133">Em seguida, *nsupdate -g* assumirão a credenciais de saudação do cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="8df20-133">Then *nsupdate -g* will pick up hello credentials from hello cache.</span></span>

<span data-ttu-id="8df20-134">Se necessário, você pode adicionar uma tooyour de sufixo de pesquisa DNS VMs.</span><span class="sxs-lookup"><span data-stu-id="8df20-134">If needed, you can add a DNS search suffix tooyour VMs.</span></span> <span data-ttu-id="8df20-135">sufixo DNS Olá é especificado em Olá */etc/resolv.conf* arquivo.</span><span class="sxs-lookup"><span data-stu-id="8df20-135">hello DNS suffix is specified in hello */etc/resolv.conf* file.</span></span> <span data-ttu-id="8df20-136">A maioria das distribuições de Linux gerenciam automaticamente o conteúdo de saudação desse arquivo, então, normalmente você não pode editá-lo.</span><span class="sxs-lookup"><span data-stu-id="8df20-136">Most Linux distros automatically manage hello content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="8df20-137">No entanto, você pode substituir o sufixo Olá por meio do cliente do DHCP Olá *substituem* comando.</span><span class="sxs-lookup"><span data-stu-id="8df20-137">However, you can override hello suffix by using hello DHCP client's *supersede* command.</span></span> <span data-ttu-id="8df20-138">toodo isso, na */etc/dhcp/dhclient.conf*, adicionar:</span><span class="sxs-lookup"><span data-stu-id="8df20-138">toodo this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

