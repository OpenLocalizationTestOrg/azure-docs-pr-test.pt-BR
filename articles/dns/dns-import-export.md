---
title: "aaaImport e uma zona de domínio de exportação de arquivo tooAzure DNS usando o Azure CLI 1.0 | Microsoft Docs"
description: Saiba como tooimport e exportar um DNS da zona tooAzure arquivo DNS usando 1.0 da CLI do Azure
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a>Importar e exportar um arquivo de zona DNS usando Olá 1.0 da CLI do Azure 

Este artigo o orienta como tooimport e exportar arquivos de zona do DNS para usar o DNS do Azure Olá 1.0 da CLI do Azure.

## <a name="introduction-toodns-zone-migration"></a>Migração de região de tooDNS de Introdução

Um arquivo de zona DNS é um arquivo de texto que contém os detalhes de cada registro do sistema de nome de domínio (DNS) na zona de saudação. Ele segue um formato padrão, tornando-o adequado para transferir registros DNS entre sistemas DNS. Usar um arquivo de zona é rápida e confiável e tootransfer de forma conveniente uma zona DNS ou de DNS do Azure.

DNS do Azure oferece suporte à importação e exportação de arquivos de zona usando hello Azure interface de linha de comando (CLI). Importação de arquivo de zona é **não** atualmente com suporte por meio do PowerShell do Azure ou hello portal do Azure.

Olá 1.0 da CLI do Azure é uma ferramenta de linha de comando de plataforma cruzada usada para gerenciar serviços do Azure. Ele está disponível para plataformas de Windows, Mac e Linux de saudação do hello [página de downloads do Azure](https://azure.microsoft.com/downloads/). Suporte de plataforma cruzada é importante para importar e exportar arquivos de zona, porque Olá software mais comuns do servidor de nome, [ASSOCIAR](https://www.isc.org/downloads/bind/), normalmente é executado no Linux.

> [!NOTE]
> Atualmente, há duas versões do hello CLI do Azure. A CLI1.0 é baseada em Node.js e tem comandos que começam com “azure”.
> A CLI2.0 é baseada em Python e tem comandos que começam com “az”. Enquanto a importação do arquivo de zona é suportada em ambas as versões, recomendamos usar comandos CLI1.0 hello, conforme descrito nesta página.

## <a name="obtain-your-existing-dns-zone-file"></a>Obtenha seu arquivo de zona DNS existente

Antes de importar um arquivo de zona do DNS no DNS do Azure, você precisa tooobtain uma cópia do arquivo de zona hello. origem desse arquivo Hello depende de onde a zona do DNS hello está hospedada no momento.

* Se a zona DNS é hospedada por um serviço de parceiro (como um registrador de domínio, provedor de hospedagem de DNS dedicado ou provedor de nuvem alternativos), esse serviço deve fornecer o arquivo de zona DNS Olá capacidade toodownload hello.
* Se a zona DNS estiver hospedada no DNS do Windows, a pasta de padrão de saudação para arquivos de zona Olá é **%systemroot%\system32\dns**. arquivo de zona Olá caminho completo tooeach também mostra no hello **geral** guia do console de saudação do DNS.
* Se a zona DNS é hospedada por meio de associação, local de saudação do arquivo de zona Olá para cada zona é especificado no arquivo de configuração de ligação de saudação **named.conf**.

> [!NOTE]
> Arquivos de zona baixados do GoDaddy têm um formato ligeiramente diferente do padrão. Você precisa toocorrect isso antes de importar esses arquivos de zona DNS do Azure.
>
> Nomes DNS em Olá RDATA de cada registro DNS são especificados como nomes totalmente qualificados, mas eles não têm um encerramento "." Isso significa que eles são interpretados por outros sistemas DNS como nomes relativos. Você precisa de arquivo para zona tooedit Olá tooappend Olá encerrando "." tootheir nomes antes de importá-los no DNS do Azure.
>
> Por exemplo, Olá registro CNAME "www 3600 CNAME contoso.com" deve ser alterada muito "www 3600 CNAME em contoso.com."
> (com uma terminação “.”).

## <a name="import-a-dns-zone-file-into-azure-dns"></a>Importar um arquivo de zona DNS para o DNS do Azure

A importação de um arquivo de zona criará uma nova zona no DNS do Azure, se ela ainda não existir. Se já existir uma zona Olá, hello conjuntos de registros no arquivo de zona Olá devem ser mesclados com conjuntos de registros existentes hello.

### <a name="merge-behavior"></a>Comportamento de mesclagem

* Por padrão, os conjuntos de registros novos e existentes são mesclados. Registros idênticos em um conjunto de registros mesclados têm a duplicação eliminada.
* Como alternativa, especificando Olá `--force` opção, Olá substitui o processo importar conjuntos de registros existentes com novos conjuntos de registros. Conjuntos de registros existentes que não tem um registro correspondente definido no arquivo de zona importada Olá não serão ser removidas.
* Quando os conjuntos de registros são mesclados, hello tempo toolive (TTL) preexistentes de conjuntos de registros é usado. Quando `--force` é usado, Olá TTL do novo conjunto de registros de saudação é usado.
* Início dos parâmetros de autoridade (SOA) (exceto `host`) sempre são extraídas do arquivo de zona importada hello, independentemente se `--force` é usado. Da mesma forma, para Olá nome servidor conjunto de registros no ápice da zona de hello, hello TTL é sempre obtida do arquivo de zona importada hello.
* Um registro CNAME importado não substitui um CNAME existente registrar com hello mesmo nome, a menos que Olá `--force` parâmetro for especificado.
* Quando um conflito entre um registro CNAME e outro registro de mesmo nome mas diferente de saudação tipo (independentemente de qual existente ou novo), registro existente Olá é mantido. Isso é independente do uso de saudação do `--force`.

### <a name="additional-information-about-importing"></a>Informações adicionais sobre importação

Olá observações a seguir fornecem detalhes técnicos adicionais sobre zona Olá o processo de importação.

* Olá `$TTL` diretiva é opcional e é suportado. Quando nenhum `$TTL` diretiva for fornecida, os registros sem um tempo de vida explícito sejam importados definir tooa TTL padrão de 3600 segundos. Quando dois registros no mesmo conjunto de registros hello especificar diferentes TTLs, valor inferior Olá é usado.
* Olá `$ORIGIN` diretiva é opcional e é suportado. Quando nenhum `$ORIGIN` for definida, o padrão de saudação valor usado é o nome da zona Olá conforme especificado na linha de comando de saudação (mais encerrando Olá ".").
* Olá `$INCLUDE` e `$GENERATE` diretivas não têm suporte.
* Há suporte aos seguintes tipos de registros: A, AAAA, CNAME, MX, NS, SOA, SRV e TXT.
* Olá registro SOA é criado automaticamente pelo DNS do Azure quando uma zona é criada. Quando você importa um arquivo de zona, todos os parâmetros SOA são extraídos do arquivo de zona Olá *exceto* Olá `host` parâmetro. Esse parâmetro usa o valor de saudação fornecida pelo DNS do Azure. Isso ocorre porque esse parâmetro deve referir-se o servidor de nome principal de toohello fornecido pelo DNS do Azure.
* registro de servidor de nomes de saudação definido no ápice da zona de saudação também é criado automaticamente pelo DNS do Azure quando Olá zona é criada. Somente hello TTL deste conjunto de registros é importado. Esses registros contêm nomes de servidor de nome hello fornecidos pelo DNS do Azure. dados de registro de saudação não são substituídos por valores hello contidos no arquivo de zona importada hello.
* Durante a visualização pública, o DNS do Azure suporta apenas os registros TXT de cadeia de caracteres única. Os registros TXT cadeias de caracteres múltiplas ser truncado e concatenado too255 caracteres.

### <a name="cli-format-and-values"></a>Valores e formato da CLI

formato Olá Olá CLI do Azure comando tooimport uma zona DNS é:

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

Valores:

* `<resource group>`é o nome de Olá Olá do grupo de recursos para a zona de saudação no DNS do Azure.
* `<zone name>`é o nome de saudação da zona de saudação.
* `<zone file name>`é Olá caminho/nome do toobe de arquivo de zona Olá importado.

Se uma zona com este nome não existe no grupo de recursos hello, ele é criado para você. Se hello zona já existir, hello conjuntos de registros importados são mesclados com conjuntos de registros existentes. toooverwrite Olá existente conjuntos de registros, use Olá `--force` opção.

formato de saudação tooverify de um arquivo de zona sem importá-lo, use Olá realmente `--parse-only` opção.

### <a name="step-1-import-a-zone-file"></a>Etapa 1. Importar um arquivo de zona

tooimport um arquivo de zona para a zona de saudação **contoso.com**.

1. Entre no tooyour assinatura do Azure usando Olá 1.0 da CLI do Azure.

    ```azurecli
    azure login
    ```

2. Selecione a assinatura de saudação onde você deseja toocreate sua nova zona DNS.

    ```azurecli
    azure account set <subscription name>
    ```

3. DNS do Azure é um serviço de Gerenciador de recursos somente do Azure, Olá CLI do Azure deve ser desligados tooResource Manager modo.

    ```azurecli
    azure config mode arm
    ```

4. Antes de usar o serviço de DNS do Azure hello, você deve registrar o provedor de recursos assinatura toouse Olá Network. (Essa operação deve ser executa apenas uma vez para cada assinatura.)

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. Se você não tiver um já, você também precisará toocreate um grupo de recursos do Gerenciador de recursos.

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. zona de saudação tooimport **contoso.com** do arquivo hello **contoso.com.txt** em uma nova zona DNS no grupo de recursos de saudação **myresourcegroup**, execute o comando de saudação `azure network dns zone import`.<BR>Esse comando carrega o arquivo de zona hello e analisá-lo. comando Olá executa uma série de comandos na zona de Olá Olá DNS do Azure serviço toocreate e conjuntos de todos os registros de saudação na zona de saudação. comando Olá relata o progresso na janela de console hello, juntamente com quaisquer erros ou avisos. Como conjuntos de registros são criados em série, pode levar alguns tooimport de minutos um arquivo grande.

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a>Etapa 2. Verifique se a zona de saudação

tooverify Olá zona DNS depois de importar o arquivo hello, você pode usar qualquer um dos métodos a seguir de saudação:

* Você pode listar os registros de saudação usando Olá após o comando CLI do Azure:

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* Você pode listar os registros de saudação usando o cmdlet do PowerShell Olá `Get-AzureRmDnsRecordSet`.
* Você pode usar `nslookup` tooverify a resolução de nomes para os registros de saudação. Como a zona de saudação não é delegada ainda, é necessário servidores de nome de DNS do Azure corretos do toospecify Olá explicitamente. Olá exemplo a seguir mostra como os nomes de servidor de nome tooretrieve Olá atribuídos toohello zona. IT também mostra como registrar o tooquery hello "www" usando `nslookup`.

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a>Etapa 3. Atualizar a delegação DNS

Depois de ter verificado que zona Olá foi importada corretamente, é necessário tooupdate Olá DNS delegação toopoint toohello Azure servidores de nome DNS. Para obter mais informações, consulte o artigo Olá [atualizar delegação de DNS Olá](dns-domain-delegation.md).

## <a name="export-a-dns-zone-file-from-azure-dns"></a>Como exportar um arquivo de zona DNS do DNS do Azure

formato Olá Olá CLI do Azure comando tooimport uma zona DNS é:

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

Valores:

* `<resource group>`é o nome de Olá Olá do grupo de recursos para a zona de saudação no DNS do Azure.
* `<zone name>`é o nome de saudação da zona de saudação.
* `<zone file name>`é Olá caminho/nome do toobe de arquivo de zona hello exportada.

Como com a importação de zona hello, primeiro é necessário toosign em, escolha sua assinatura e configurar o modo de Gerenciador de recursos de toouse Olá CLI do Azure.

### <a name="tooexport-a-zone-file"></a>tooexport um arquivo de zona

1. Entre no tooyour assinatura do Azure usando Olá CLI do Azure.

    ```azurecli
    azure login
    ```

2. Selecione a assinatura Olá onde você deseja toocreate a zona DNS.

    ```azurecli
    azure account set <subscription name>
    ```

3. O Azure DNS é um serviço somente do Gerenciador de Recursos do Azure. Olá CLI do Azure deve ser desligados tooResource Manager modo.

    ```azurecli
    azure config mode arm
    ```

4. tooexport Olá zona DNS do Azure existente **contoso.com** no grupo de recursos **myresourcegroup** toohello arquivo **contoso.com.txt** (na Olá atual pasta), execute `azure network dns zone export`. Esse comando chamadas Olá tooenumerate de serviço DNS do Azure conjuntos de registro na zona hello e exportar o arquivo de zona do hello resultados tooa compatível com o BIND.

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
