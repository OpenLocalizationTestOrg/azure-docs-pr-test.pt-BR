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
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a>Usando nomes de host DNS dinâmico tooregister em seu próprio servidor DNS
[Azure fornece resolução de nomes](virtual-networks-name-resolution-for-vms-and-role-instances.md) para VMs (máquinas virtuais) e instâncias de função. Contudo, quando a resolução de nome precisar ir além do que é fornecido pelo Azure, você pode fornecer seus próprios servidores DNS. Isso dá a você Olá power tootailor seu toosuit de solução DNS suas necessidades específicas. Por exemplo, talvez seja necessário tooaccess recursos de locais por meio do controlador de domínio do Active Directory.

Quando seus servidores DNS personalizados são hospedados como máquinas virtuais do Azure que você pode encaminhar hostname consulta Olá mesmo vnet tooAzure tooresolve nomes de host. Se você não desejar toouse essa rota, você pode registrar seu nome de host VM no seu servidor DNS usando DNS dinâmico.  Azure não tem Olá capacidade (por exemplo, credenciais) toodirectly criar registros em seus servidores DNS, para que organizações alternativas costumam ser necessárias. Aqui estão alguns cenários comuns com alternativas.

## <a name="windows-clients"></a>Clientes do Windows
Clientes do Windows não unidos por domínio tentam atualizações não seguras de DNS dinâmico (DDNS) quando eles são inicializados ou quando seu endereço IP for alterado. nome DNS de saudação é hostname hello mais sufixo DNS primário de saudação. Azure deixa o sufixo DNS primário de saudação em branco, mas você pode definir isso em Olá VM, por meio de saudação [UI](https://technet.microsoft.com/library/cc794784.aspx) ou [usando automação](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).

Clientes do Windows ingressado no domínio registrem seus endereços IP com o controlador de domínio hello usando DNS dinâmico seguro. processo de associação de domínio Olá define o sufixo DNS primário Olá no cliente de saudação e cria e mantém a relação de confiança de saudação.

## <a name="linux-clients"></a>Clientes Linux
Os clientes do Linux geralmente não se registraram com o servidor DNS Olá na inicialização, ele assume um servidor DHCP de saudação faz isso. Os servidores DHCP do Azure não tem capacidade de saudação ou registros de tooregister de credenciais no seu servidor DNS.  Você pode usar uma ferramenta chamada *nsupdate*, que está incluído no pacote de ligação hello, atualizações de DNS dinâmico toosend. Olá protocolo DNS dinâmico é padronizado, você pode usar *nsupdate* mesmo quando você não estiver usando Bind no servidor DNS hello.

Você pode usar ganchos de saudação que são fornecidos pelo toocreate de cliente DHCP hello e manter Olá entrada de nome de host do servidor DNS de saudação. Durante o ciclo DHCP Olá, o cliente de saudação executa scripts Olá */etc/dhcp/dhclient-exit-hooks.d/*. Isso pode ser usado tooregister Olá novo endereço IP usando *nsupdate*. Por exemplo:

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

        
        

Você também pode usar o hello *nsupdate* tooperform de comando de atualizações de DNS dinâmico seguro. Por exemplo, quando você estiver usando um servidor DNS de associação, um par de chaves públicas-privadas será [gerado](http://linux.yyz.us/nsupdate/).  servidor de DNS Olá [configurado](http://linux.yyz.us/dns/ddns-server.html) com a parte pública de saudação da chave Olá para que ele possa verificar se a assinatura de saudação na solicitação de saudação. Você deve usar o hello *-k* tooprovide opção Olá par de chaves muito*nsupdate* em ordem para Olá toobe solicitação assinado de atualização de DNS dinâmico.

Quando você estiver usando um servidor DNS do Windows, você pode usar a autenticação Kerberos com hello *-g* parâmetro em *nsupdate* (não disponível na versão do Windows de saudação *nsupdate* ). toodo isso, use *kinit* credenciais de saudação tooload (por exemplo, de um [arquivo keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)). Em seguida, *nsupdate -g* assumirão a credenciais de saudação do cache de saudação.

Se necessário, você pode adicionar uma tooyour de sufixo de pesquisa DNS VMs. sufixo DNS Olá é especificado em Olá */etc/resolv.conf* arquivo. A maioria das distribuições de Linux gerenciam automaticamente o conteúdo de saudação desse arquivo, então, normalmente você não pode editá-lo. No entanto, você pode substituir o sufixo Olá por meio do cliente do DHCP Olá *substituem* comando. toodo isso, na */etc/dhcp/dhclient.conf*, adicionar:

        supersede domain-name <required-dns-suffix>;

