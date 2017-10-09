---
title: aaaViewing e modificar os nomes de host | Microsoft Docs
description: "Como tooview e altere os nomes de host para máquinas virtuais do Azure, web e funções de trabalho para a resolução de nome"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 17d0dd7911754a94db3f37b924b4687da1c70aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="viewing-and-modifying-hostnames"></a>Exibindo e modificando os nomes do host
tooallow seu toobe de instâncias de função referenciada por nome do host, você deve definir o valor de saudação para o nome de host Olá no arquivo de configuração de serviço Olá para cada função. Você pode fazer isso adicionando toohello de nome de host de saudação desejada **vmName** atributo de saudação **função** elemento. Olá valor Olá **vmName** atributo é usado como base para o nome de host de saudação de cada instância de função. Por exemplo, se **vmName** é *webrole* e houver três instâncias dessa função, os nomes de host de saudação de instâncias de saudação será *webrole0*, *webrole1* , e *webrole2*. Não é necessário toospecify um nome de host para máquinas virtuais no arquivo de configuração hello, porque o nome do host Olá para uma máquina virtual é preenchido com base no nome da máquina virtual hello. Para obter mais informações sobre como configurar um serviço do Microsoft Azure, consulte [Esquema de configuração do serviço do Azure (arquivo .cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx)

## <a name="viewing-hostnames"></a>Exibindo nomes do host
Você pode exibir os nomes de host de saudação de máquinas virtuais e instâncias de função em um serviço de nuvem usando qualquer uma das ferramentas de saudação abaixo.

### <a name="azure-portal"></a>Portal do Azure
Você pode usar o hello [portal do Azure](http://portal.azure.com) tooview nomes de host Olá para máquinas virtuais na folha de visão geral de saudação para uma máquina virtual. Tenha em mente que Olá folha mostra um valor para **nome** e **nome de Host**. Embora inicialmente sejam Olá iguais, a alteração de nome de host de saudação não alterará Olá nome da máquina virtual de saudação ou instância de função.

Instâncias de função também podem ser exibidas no hello portal do Azure, mas ao listar as instâncias de saudação em um serviço de nuvem, o nome de host de saudação não é exibido. Você verá um nome para cada instância, mas esse nome não representa o nome do host de saudação.

### <a name="service-configuration-file"></a>Arquivo de configuração de serviço
Você pode baixar o arquivo de configuração do serviço de saudação para um serviço implantado do hello **configurar** lâmina de serviço Olá Olá portal do Azure. Em seguida, procure Olá **vmName** atributo Olá **nome da função** nome de host do elemento toosee hello. Tenha em mente que esse nome de host é usado como base para o nome de host de saudação de cada instância de função. Por exemplo, se **vmName** é *webrole* e houver três instâncias dessa função, os nomes de host de saudação de instâncias de saudação será *webrole0*, *webrole1* , e *webrole2*.

### <a name="remote-desktop"></a>Área de Trabalho Remota
Depois de habilitar a área de trabalho remota (Windows), comunicação remota do Windows PowerShell (Windows) ou máquinas virtuais do SSH (Linux e Windows) conexões tooyour ou instâncias de função, você pode exibir o nome de host de saudação de uma conexão de área de trabalho remota ativa de várias maneiras:

* Digite o nome do host no prompt de comando de saudação ou terminal SSH.
* Digite ipconfig/todos no comando Olá prompt (somente Windows).
* Nome do computador do modo de exibição Olá no sistema Olá configurações (somente Windows).

### <a name="azure-service-management-rest-api"></a>API REST de Gerenciamento de Serviços do Azure
Em um cliente REST, siga estas instruções:

1. Certifique-se de que você tenha um toohello de tooconnect de certificado de cliente portal do Azure. tooobtain um certificado de cliente, execute as etapas de saudação apresentadas em [como: baixar e importar configurações de publicação e informações de assinatura](https://msdn.microsoft.com/library/dn385850.aspx). 
2. Defina uma entrada de cabeçalho chamada x-ms-version com um valor de 2013-11-01.
3. Enviar uma solicitação no hello formato a seguir: https://management.core.windows.net/\<esta opção-id\>/services/hostedservices/\<nome do serviço\>? detalhes incorporar = true
4. Procure Olá **HostName** elemento para cada **RoleInstance** elemento.

> [!WARNING]
> Você também pode exibir o sufixo de domínio interno Olá para seu serviço de nuvem do hello resposta de chamada REST verificando Olá **InternalDnsSuffix** elemento, ou executando ipconfig/tudo a partir de um prompt de comando em uma sessão de área de trabalho remota (Windows) ou, em execução /etc/resolv.conf cat de um terminal SSH (Linux).
> 
> 

## <a name="modifying-a-hostname"></a>Modificando um nome de host
Você pode modificar o nome de host de saudação para qualquer máquina virtual ou instância de função carregando um arquivo de configuração do serviço modificado ou renomeando computador saudação de uma sessão de área de trabalho remota.

## <a name="next-steps"></a>Próximas etapas
[Resolução de nomes (DNS)](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[Esquema de configuração de serviço do Azure (.cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[Esquema de configuração de Rede Virtual do Azure](http://go.microsoft.com/fwlink/?LinkId=248093)

[Especificar configurações de DNS usando arquivos de configuração de rede](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)

