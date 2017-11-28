---
title: "aaaSQL VM conexão tooAzure pesquisa | Microsoft Docs"
description: "Habilitar conexões criptografadas e configurar Olá firewall tooallow conexões tooSQL Server em uma máquina virtual (VM) do Azure de um indexador na pesquisa do Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: pablocas
editor: 
ms.assetid: 46e42e0e-c8de-4fec-b11a-ed132db7e7bc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: heidist
ms.openlocfilehash: 1f0db8a2812b0a7d012e58bb873c4b2b29fa1338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-connection-from-an-azure-search-indexer-toosql-server-on-an-azure-vm"></a>Configurar uma conexão de um indexador de pesquisa do Azure tooSQL Server em uma VM do Azure
Conforme observado na [tooAzure conectando o Azure SQL Database pesquisar usando indexadores](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md#faq), criando indexadores contra **do SQL Server em máquinas virtuais do Azure** (ou **VMs do SQL Azure** abreviada) é com suporte de pesquisa do Azure, mas há alguns tootake pré-requisitos relacionados à segurança respeito primeiro. 

**Duração da tarefa:** cerca de 30 minutos, supondo que você já instalou um certificado em Olá VM.

## <a name="enable-encrypted-connections"></a>Habilitar conexões criptografadas
O Azure Search requer um canal criptografado para todas as solicitações de indexador em uma conexão de Internet pública. Esta seção lista Olá etapas toomake esse trabalho.

1. Verifique as propriedades de saudação do nome da entidade Olá Olá certificado tooverify nome de domínio totalmente qualificado (FQDN) Olá de saudação VM do Azure. Você pode usar uma ferramenta como CertUtils ou Olá certificados snap-in tooview Olá propriedades. Você pode obter Olá FQDN de Essentials seção da folha de serviço para a VM Olá, Olá **rótulo de nome de DNS/endereço IP público** campo, Olá [portal do Azure](https://portal.azure.com/).
   
   * Para máquinas virtuais criadas usando hello mais recente **Gerenciador de recursos de** modelo, Olá FQDN é formatada como `<your-VM-name>.<region>.cloudapp.azure.com`. 
   * Para máquinas virtuais mais antigas criadas como um **clássico** VM, Olá FQDN é formatado como `<your-cloud-service-name.cloudapp.net>`. 
2. Configure certificado do SQL Server toouse hello usando Olá Editor do registro (regedit). 
   
    Embora o SQL Server Configuration Manager seja geralmente usado para essa tarefa, você não pode usá-lo para esse cenário. Ele não localizará Olá certificado importado porque Olá FQDN do hello VM no Azure não corresponde a saudação FQDN, conforme determinado pela Olá VM (ele identifica domínio hello como computador local hello ou Olá toowhich de domínio de rede que são Unidos). Quando nomes não corresponderem, use o certificado de saudação do regedit toospecify.
   
   * Regedit, procurar a chave de registro toothis: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\[MSSQL13.MSSQLSERVER]\MSSQLServer\SuperSocketNetLib\Certificate`.
     
     Olá `[MSSQL13.MSSQLSERVER]` parte varia com base no nome de instância e versão. 
   * Definir valor Olá Olá **certificado** toohello chave **impressão digital** do certificado SSL Olá importado toohello VM.
     
     Há várias maneiras tooget Olá impressão digital alguns melhor do que outros. Se você o copiar de saudação **certificados** snap-in no MMC, você provavelmente escolherá um caractere à esquerda invisível [conforme descrito neste artigo de suporte](https://support.microsoft.com/kb/2023869/), que resulta em um erro durante a tentativa de um conexão. Existem várias soluções alternativas para corrigir esse problema. Olá mais fácil é toobackspace e digite primeiro caractere Olá Olá impressão digital tooremove Olá caractere à esquerda no campo de valor de chave Olá Regedit. Como alternativa, você pode usar uma impressão digital Olá de toocopy ferramenta diferente.
3. Conceda permissões de conta de serviço toohello. 
   
    Certifique-se de Olá conta de serviço do SQL Server é concedido permissão apropriada na chave privada de saudação do certificado SSL da saudação. Se você ignorar essa etapa, o SQL Server não será iniciado. Você pode usar o hello **certificados** snap-in ou **CertUtils** para esta tarefa.
4. Reinicie o serviço do SQL Server hello.

## <a name="configure-sql-server-connectivity-in-hello-vm"></a>Configurar a conectividade do SQL Server na VM de saudação
Depois de configurar a conexão de saudação criptografada requerido pela pesquisa do Azure, há uma configuração adicional de etapas intrínseco tooSQL Server em VMs do Azure. Se você ainda não tiver feito isso, Olá próxima etapa é toofinish configuração usando um dos seguintes artigos:

* Para uma **Gerenciador de recursos de** VM, consulte [tooa Máquina Virtual do SQL Server no Azure usando o Gerenciador de recursos de conexão](../virtual-machines/windows/sql/virtual-machines-windows-sql-connect.md). 
* Para uma **clássico** VM, consulte [conectar tooa Máquina Virtual do SQL Server no Azure clássico](../virtual-machines/windows/classic/sql-connect.md).

Em particular, consulte a seção de saudação cada artigo para "conectar-se via Olá internet".

## <a name="configure-hello-network-security-group-nsg"></a>Configurar Olá grupo de segurança de rede (NSG)
Não é incomum tooconfigure Olá NSG e ponto de extremidade do Azure correspondente ou lista de controle de acesso (ACL) toomake partes de tooother acessível sua VM do Azure. A probabilidade é que fazer isso antes de tooallow sua própria tooyour de tooconnect de lógica de aplicativo VM do SQL Azure. Ele não é diferente para uma conexão de pesquisa do Azure tooyour VM do SQL Azure. 

Olá links a seguir fornecem instruções sobre configuração de NSG para implantações de VM. Use estas instruções que tooacl um ponto de extremidade de pesquisa do Azure com base em seu endereço IP.

> [!NOTE]
> Para saber mais, consulte [O que é um Grupo de Segurança de Rede?](../virtual-network/virtual-networks-nsg.md)
> 
> 

* Para uma **Gerenciador de recursos de** VM, consulte [como toocreate NSGs para implantações de ARM](../virtual-network/virtual-networks-create-nsg-arm-pportal.md). 
* Para uma **clássico** VM, consulte [como toocreate NSGs para implantações clássico](../virtual-network/virtual-networks-create-nsg-classic-ps.md).

Endereçamento IP pode representar alguns desafios que são superados facilmente se você está ciente do problema hello e possíveis soluções alternativas. seções restantes Olá fornecem recomendações para lidar com problemas relacionados tooIP endereços Olá ACL.

#### <a name="restrict-access-toohello-search-service-ip-address"></a>Restringir o endereço IP do serviço de pesquisa de toohello de acesso
É altamente recomendável que você restrinja Olá acesso toohello endereço do seu serviço de pesquisa no hello ACL em vez de fazer suas VMs do SQL Azure totalmente aberta tooany solicitações de conexão. Você pode facilmente descobrir Olá IP endereço usando o comando ping Olá FQDN (por exemplo, `<your-search-service-name>.search.windows.net`) do seu serviço de pesquisa.

#### <a name="managing-ip-address-fluctuations"></a>Gerenciando flutuações de endereço IP
Se o serviço de pesquisa tem apenas uma unidade de pesquisa (ou seja, uma réplica e uma partição), o endereço IP de saudação será alterado durante a manutenção de rotina for reiniciado, invalidando a uma ACL existente com o endereço IP do seu serviço de pesquisa.

Erro na conectividade subsequentes Olá tooavoid unidirecional é toouse mais de uma réplica e uma partição na pesquisa do Azure. Isso aumenta o custo de hello, mas ele também resolve o problema de saudação de endereço IP. No Azure Search, os endereços IP não são alterados quando você tiver mais de uma unidade de pesquisa.

Uma segunda abordagem é tooallow Olá conexão toofail e, em seguida, reconfigurar Olá ACLs em Olá NSG. Em média, você pode esperar toochange de endereços IP em algumas semanas. Para clientes que fazem a indexação controlada raramente, essa abordagem pode ser viável.

Uma terceira abordagem viável (mas não muito segura) é o intervalo de endereços IP toospecify Olá de saudação região do Azure em que o serviço de pesquisa é provisionado. saudação de lista de intervalos IP do qual os endereços IP públicos tooAzure os recursos são alocados é publicada na [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653). 

#### <a name="include-hello-azure-search-portal-ip-addresses"></a>Incluir endereços IP portais Olá pesquisa do Azure
Se você estiver usando Olá toocreate portal do Azure um indexador, lógica de portal de pesquisa do Azure também precisa de acesso tooyour SQL Azure VM durante o tempo de criação. Os endereços IP do portal do Azure Search podem ser encontrados executando ping de `stamp2.search.ext.azure.com`.

## <a name="next-steps"></a>Próximas etapas
Com a configuração do caminho de saudação, agora você pode especificar um SQL Server na VM do Azure como fonte de dados de saudação para um indexador da pesquisa do Azure. Consulte [tooAzure conectando o Azure SQL Database pesquisar usando indexadores](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md) para obter mais informações.

