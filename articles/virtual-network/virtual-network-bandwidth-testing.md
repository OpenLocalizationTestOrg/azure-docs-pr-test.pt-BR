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
# <a name="bandwidththroughput-testing-ntttcp"></a>Teste de Largura de Banda/Taxa de Transferência (NTTTCP)

Ao testar o desempenho de taxa de transferência de rede no Azure, é melhor toouse uma ferramenta que tem como alvo a rede Olá para teste e minimiza o uso de saudação de outros recursos que podem afetar o desempenho. É recomendável usar o NTTTCP.

Copiar Olá ferramenta tootwo VMs do Azure de saudação mesmo tamanho. Uma máquina virtual funciona como remetente e hello como destinatário.

#### <a name="deploying-vms-for-testing"></a>Implantando VMs para teste
Para fins de saudação desse teste, Olá duas VMs devem estar no Olá mesmo serviço de nuvem ou Olá mesmo conjunto de disponibilidade para que possamos pode usar os IPs internos e excluir Olá balanceadores de carga de teste de saudação. É possível tootest com hello VIP, mas esse tipo de teste está fora do escopo deste documento hello.
 
Tome nota do endereço IP do destinatário hello. Vamos chamar esse IP de “a.b.c.r”

Anote Olá número de núcleos na VM de saudação. Vamos chamar isso de “\#num\_cores”
 
Execute Olá NTTTCP de teste para 300 segundos (ou 5 minutos) no remetente Olá VM e o destinatário VM.

Dica: Ao configurar este teste para Olá primeira vez, você pode tentar um comentário de tooget período mais curto do teste mais cedo. Depois que a ferramenta hello está funcionando conforme o esperado, estenda segundos de too300 período de teste Olá para obter resultados mais precisos hello.

> [!NOTE]
> remetente Olá **e** receptor deve especificar **Olá mesmo** parâmetro de duração de teste (-t).

tootest um único fluxo TCP 10 segundos:

Parâmetros do receptor: ntttcp -r -t 10 -P 1

Parâmetros do remetente: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1

> [!NOTE]
> Olá anterior exemplo só deve ser usado tooconfirm sua configuração. Exemplos válidos de teste são abordados adiante neste documento.

## <a name="testing-vms-running-windows"></a>Testando VMs que executam o WINDOWS:

#### <a name="get-ntttcp-onto-hello-vms"></a>Obter NTTTCP para Olá VMs.

Baixar a versão mais recente do hello: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769>

Se preferir, pesquise-a, caso tenha sido movida: <https://www.bing.com/search?q=ntttcp+download>\< – deve ser a primeira ocorrência

Considere colocar o NTTTCP em uma pasta separada, como c:\\tools

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a>Permitir NTTTCP através do firewall do Windows hello
No hello RECEPTOR, crie uma regra de permissão tooallow do Firewall do Windows hello tooarrive de tráfego de NTTTCP. É mais fácil tooallow Olá NTTTCP programa inteiro por nome em vez de tooallow portas TCP de entrada.

Permitir ntttcp por meio de saudação Firewall do Windows como este:

netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

Por exemplo, se você copiou ntttcp.exe toohello "c:\\ferramentas" pasta, isso seria comando hello: 

netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

#### <a name="running-ntttcp-tests"></a>Executando testes NTTTCP

Iniciar NTTTCP em Olá RECEPTOR (**executar de CMD**, não do PowerShell):

ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300

Se Olá VM tem quatro núcleos e um endereço IP de 10.0.0.4, ele teria esta aparência:

ntttcp -r –m 8,\*,10.0.0.4 -t 300


Iniciar NTTTCP em Olá remetente (**executar de CMD**, não do PowerShell):

ntttcp -s –m 8,\*,10.0.0.4 -t 300 

Aguarde até que os resultados de saudação.


## <a name="testing-vms-running-linux"></a>Testando VMs que executam o LINUX:

Use nttcp-for-linux. Ele está disponível em <https://github.com/Microsoft/ntttcp-for-linux>

No hello VMs do Linux (remetente e destinatário), execute estes comandos para preparar ntttcp para linux em suas VMs:

CentOS – Instalar o Git:
``` bash
  yum install gcc -y  
  yum install git -y
```
Ubuntu – Instalar o Git:
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
Crie e instale nas duas:
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

Como exemplo do Windows hello, vamos supor que IP do RECEPTOR de Linux Olá será 10.0.0.4

Inicie NTTTCP para Linux em Olá destinatário:

``` bash
ntttcp -r -t 300
```

E em Olá remetente, execute:

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
Teste comprimento padrão é too60 segundos se nenhum parâmetro de tempo é fornecido

## <a name="testing-between-vms-running-windows-and-linux"></a>Testar entre VMs executando o Windows e LINUX:

Este cenários é deve habilitar o modo de sincronização não Olá para que teste Olá possa ser executados. Isso é feito usando Olá **sinalizador -N** para Linux e **sinalizador -ns** para Windows.

#### <a name="from-linux-toowindows"></a>De tooWindows Linux:

Receptor <Windows>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

Remetente <Linux> :

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a>Do Windows tooLinux:

Receptor <Linux>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

Remetente <Windows>:

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a>Próximas etapas
* Dependendo de resultados, pode haver espaço muito[otimizar máquinas de taxa de transferência de rede](virtual-network-optimize-network-bandwidth.md) para seu cenário.
* Saiba mais com as [Perguntas frequentes sobre a Rede Virtual do Azure](virtual-networks-faq.md)
