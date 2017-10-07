---
title: "aaaManage registros DNS no DNS do Azure usando Olá 1.0 da CLI do Azure | Microsoft Docs"
description: "Gerenciando conjuntos de registros DNS e registros no DNS do Azure ao hospedar seu domínio no DNS do Azure. Todos os comandos da CLI 1.0 para operações em conjuntos de registros e registros."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 1f01450b0839f712cb1d96be318766bac581fea1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-in-azure-dns-using-hello-azure-cli-10"></a>Gerenciar registros DNS no DNS do Azure usando Olá 1.0 da CLI do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](dns-operations-recordsets-portal.md)
> * [CLI 1.0 do Azure](dns-operations-recordsets-cli-nodejs.md)
> * [CLI 2.0 do Azure](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Este artigo mostra como toomanage registros DNS para a zona DNS usando Olá plataforma cruzada do Azure interface de linha de comando (CLI), que está disponível para Windows, Mac e Linux. Você também pode gerenciar seus registros DNS usando [Azure PowerShell](dns-operations-recordsets.md) ou hello [portal do Azure](dns-operations-recordsets-portal.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete

Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

* [1.0 de CLI do Azure](dns-operations-recordsets-cli-nodejs.md) -nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de hello.
* [2.0 do CLI do Azure](dns-operations-recordsets-cli.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação.

exemplos de saudação neste artigo presumem que você já tiver [instalado hello Azure CLI 1.0, conectado e criar uma zona DNS](dns-operations-dnszones-cli-nodejs.md).

## <a name="introduction"></a>Introdução

Antes de criar os registros DNS no DNS do Azure, primeiro é necessário toounderstand como o DNS do Azure organiza os registros DNS em conjuntos de registros de DNS.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Para obter mais informações sobre os registros DNS no DNS do Azure, confira [Zonas e registros DNS](dns-zones-records.md).

## <a name="create-a-dns-record"></a>Criar um registro DNS

toocreate um registro DNS, use Olá `azure network dns record-set add-record` comando. Para obter ajuda, consulte `azure network dns record-set add-record -h`.

Ao criar um registro, é necessário o nome do grupo de recursos do toospecify Olá, nome da zona, conjunto de registros, nome, tipo de registro de saudação e detalhes de saudação do registro de hello está sendo criado. Olá nome do conjunto de registros fornecido deve ser um *relativo* nome, o que significa que ele deve excluir o nome da zona hello.

Se o conjunto de registros de saudação ainda não existir, este comando criará para você. Se já existir um conjunto de registros de hello, este comando denomine Olá registro que você especificar o conjunto de registros existentes toohello.

Se um novo conjunto de registros for criado, um TTL padrão de 3600 será usado. Para obter instruções sobre como toouse TTLs diferentes, consulte [criar um conjunto de registros de DNS](#create-a-dns-record-set).

Olá, exemplo a seguir cria um registro chamado *www* na zona Olá *contoso.com* no grupo de recursos de saudação *MyResourceGroup*. Olá Olá é um registro de endereço IP *1.2.3.4*.

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

toocreate um registro no ápice da saudação da zona de saudação (nesse caso, "contoso.com"), use o nome do registro hello "@", incluindo Olá aspas:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a>Criar um conjunto de registros DNS

Em Olá acima exemplos, registro DNS Olá era o tooan adicionado existente de conjunto de registros ou conjunto de registros de saudação foi criado *implicitamente*. Você também pode criar o conjunto de registros de saudação *explicitamente* antes de adicionar registros tooit. DNS do Azure oferece suporte a conjuntos de registros 'empty', que podem agir como um espaço reservado tooreserve um nome DNS antes de criar registros DNS. Conjuntos de registros vazios são visíveis em Olá DNS do Azure plano de controle, mas não aparecem nos servidores de nome DNS do Azure hello.

Conjuntos de registros são criados usando Olá `azure network dns record-set create` comando. Para obter ajuda, consulte `azure network dns record-set create -h`.

Criar registro Olá definido explicitamente permite toospecify propriedades de conjunto de registros como Olá [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) e metadados. [Metadados de conjunto de registros](dns-zones-records.md#tags-and-metadata) podem ser dados específicos do aplicativo de tooassociate usado com cada conjunto de registros, como pares chave-valor.

Olá, exemplo a seguir cria um registro vazio definido com um TTL de 60 segundos, por meio de saudação `--ttl` parâmetro (forma abreviada `-l`):

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

Olá, exemplo a seguir cria um conjunto de registros com duas entradas de metadados, "dept = Finanças" e "ambiente = produção", usando Olá `--metadata` parâmetro (forma abreviada `-m`):

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

Depois de criar um conjunto de registros vazio, registros podem ser adicionados usando `azure network dns record-set add-record` conforme descrito em [Criar um registro DNS](#create-a-dns-record).

## <a name="create-records-of-other-types"></a>Criar outros tipos de registro

Depois de ter visto em detalhes como registros toocreate 'A', Olá seguintes exemplos mostram como suporte para registro de toocreate de outros tipos de registro DNS do Azure.

parâmetros de saudação usados toospecify registro de saudação dados variar dependendo do tipo de saudação do registro hello. Por exemplo, para um registro do tipo "A", você especificar endereço Olá IPv4 com parâmetro hello `-a <IPv4 address>`. Olá parâmetros para cada tipo de registro pode ser listado usando `azure network dns record-set add-record -h`.

Em cada caso, mostramos como toocreate um único registro. registro de saudação é adicionado toohello existente de conjunto de registros ou um conjunto de registros criado implicitamente. Para obter mais informações sobre como criar conjuntos de registros e definir o parâmetro do conjunto de registros explicitamente, consulte [Criar um conjunto de registros DNS](#create-a-dns-record-set).

Não fornecemos um exemplo toocreate um conjunto de registros SOA, como SOAs são criados e excluídos com cada zona DNS e não pode ser criado ou excluído separadamente. No entanto, [Olá SOA pode ser modificado, conforme mostrado no exemplo mais adiante](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record"></a>Criar um registro AAAA

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a>Criar um registro CNAME

> [!NOTE]
> padrões DNS Olá não permitem que os registros CNAME no ápice da saudação de uma zona (`-Name "@"`), nem eles permitem que os conjuntos de registro que contém mais de um registro.
> 
> Para obter mais informações, consulte [Registros CNAME](dns-zones-records.md#cname-records).

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a>Criar um registro MX

Neste exemplo, podemos usar o nome do conjunto de registros de hello "@" hello toocreate registro MX no ápice da zona de saudação (nesse caso, "contoso.com").

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a>Criar um registro NS

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a>Criar um registro PTR

Nesse caso, ' Meu-arpa-zone.com' representa Olá zona ARPA que representa o intervalo de IP. Cada registro PTR definido nesta zona corresponde endereço IP tooan dentro desse intervalo IP.  nome do registro Olá '10' é último octeto saudação do endereço IP hello dentro desse intervalo IP representado por esse registro.

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a>Criar um registro SRV

Ao criar um [conjunto de registros SRV](dns-zones-records.md#srv-records), especificar Olá  *\_service* e  *\_protocolo* em Olá nome de conjunto de registros. Não há nenhuma necessidade tooinclude "@" no hello registro de nome do conjunto quando criar um registro SRV definida no ápice da zona de saudação.

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a>Criar um registro TXT

Olá exemplo a seguir mostra como registrar o toocreate um TXT. Para obter mais informações sobre Olá tamanho máximo com suporte no registros TXT, consulte [registros TXT](dns-zones-records.md#txt-records).

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a>Obter um conjunto de registros

tooretrieve um conjunto de registros existente, use `azure network dns record-set show`. Para obter ajuda, consulte `azure network dns record-set show -h`.

Ao criar um conjunto de registros ou de registro, registro Olá definir nome fornecido deve ser um *relativo* nome, o que significa que ele deve excluir o nome da zona hello. Também é necessário o tipo de registro toospecify hello, zona Olá contendo Olá registro definido e Olá que contém a zona de saudação do grupo de recursos.

Olá, exemplo a seguir recupera o registro de saudação *www* de um tipo de zona *contoso.com* no grupo de recursos *MyResourceGroup*:

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a>Listar os conjuntos de registros

Você pode listar todos os registros em uma zona DNS usando Olá `azure network dns record-set list` comando. Para obter ajuda, consulte `azure network dns record-set list -h`.

Este exemplo retorna conjuntos de todos os registros na zona Olá *contoso.com*, no grupo de recursos *MyResourceGroup*, independentemente do nome ou tipo de registro:

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

Este exemplo retorna todos os conjuntos de registros que correspondem a saudação considerando o tipo de registro (nesse caso, 'A' registros):

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-tooan-existing-record-set"></a>Adicionar um registro tooan existente de conjunto de registros

Você pode usar `azure network dns record-set add-record` tanto toocreate um registro em um novo registro ou definidas tooadd um registro existente tooan registro.

Para obter mais informações, consulte [Criar um registro DNS](#create-a-dns-record) e [Criar registros de outros tipos](#create-records-of-other-types), acima.

## <a name="remove-a-record-from-an-existing-record-set"></a>Remover um registro de um conjunto de registros existente.

registrar tooremove um DNS de um conjunto de registros existente, use `azure network dns record-set delete-record`. Para obter ajuda, consulte `azure network dns record-set delete-record -h`.

Esse comando exclui um registro DNS de um conjunto de registros. Se o último registro de saudação em um conjunto de registros é excluído, o registro de saudação definido em si é **não** excluído. Em vez disso, um conjunto de registros vazio é mantido. registro de saudação toodelete definido em vez disso, consulte [excluir um conjunto de registros](#delete-a-record-set).

Você precisa toospecify Olá toobe registro excluído e zona Olá deve ser excluída, usando Olá os mesmos parâmetros durante a criação de um registro usando `azure network dns record-set add-record`. Esses parâmetros são descritos em [Criar um registro DNS](#create-a-dns-record) e [Criar registros de outros tipos](#create-records-of-other-types), acima.

Esse comando solicita uma confirmação. Esse aviso pode ser suprimido Olá `--quiet` alternar (forma abreviada `-q`).

Olá exclusões de exemplo a seguir Olá um registro com o valor '1.2.3.4' do registro Olá conjunto nomeado *www* na zona Olá *contoso.com*, no grupo de recursos de saudação *MyResourceGroup*. prompt de confirmação de saudação é suprimida.

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a>Modificar um conjunto de registros existente

Cada conjunto de registros contém um [TTL (vida útil)](dns-zones-records.md#time-to-live), [metadados](dns-zones-records.md#tags-and-metadata) e registros DNS. Olá seções a seguir explicam como toomodify essas propriedades.

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a>toomodify um registro A, AAAA, MX, NS, PTR, SRV ou TXT

toomodify um registro existente do tipo A, AAAA, MX, NS, PTR, SRV ou TXT, você primeiro deve adicionar um novo registro e, em seguida, excluir o registro existente hello. Para obter instruções detalhadas sobre como toodelete e adicionar registros, consulte Olá seções anteriores deste artigo.

saudação de exemplo a seguir mostra como toomodify um registro de 'A', do IP endereço 1.2.3.4 tooIP endereço 5.6.7.8:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="toomodify-a-cname-record"></a>toomodify um registro CNAME

toomodify um registro CNAME, use `azure network dns record-set add-record` tooadd Olá novo valor de registro. Ao contrário de outros tipos de registro, um conjunto de registros CNAME pode conter apenas um único registro. Portanto, o registro existente Olá é *substituído* quando Olá novo registro é adicionado e não precisa toobe excluído separadamente.  Você será solicitado tooaccept essa substituição.

exemplo Hello modifica conjunto de registros de CNAME Olá *www* na zona Olá *contoso.com*, no grupo de recursos *MyResourceGroup*, toopoint muito www.fabrikam.net em vez de seu valor existente:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a>toomodify um registro SOA

Use `azure network dns record-set set-soa-record` toomodify Olá SOA para uma zona DNS. Para obter ajuda, consulte `azure network dns record-set set-soa-record -h`.

Olá exemplo a seguir mostra como propriedade tooset Olá 'email' de saudação SOA registrar para a zona de saudação *contoso.com* no grupo de recursos de saudação *MyResourceGroup*:

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="toomodify-ns-records-at-hello-zone-apex"></a>toomodify NS registros no ápice da zona de saudação

registro de NS Olá definido no ápice da zona de saudação é criado automaticamente com cada zona DNS. Ela contém nomes de saudação da zona do hello Azure DNS nome servidores toohello atribuído.

Você pode adicionar nome adicionais servidores toothis NS conjunto de registros, toosupport co-hospedagem domínios com mais de um provedor DNS. Você também pode modificar hello TTL e metadados para esse conjunto de registros. No entanto, você não pode remover ou modificar servidores de nome DNS do Azure preenchidos previamente hello.

Observe que isso se aplica apenas toohello NS conjunto de registros no ápice da zona de saudação. Outros conjuntos de registros NS na zona (como zonas de filho usado toodelegate) podem ser modificados sem restrição.

saudação de exemplo a seguir mostra como tooadd um registro NS de toohello de servidor de nome adicionais definir no ápice da zona de saudação:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a>Definir toomodify Olá TTL de um registro existente

Definir toomodify Olá TTL de um registro existente, use `azure network dns record-set set`. Para obter ajuda, consulte `azure network dns record-set set -h`.

saudação de exemplo a seguir mostra como toomodify um conjunto de registros TTL, neste caso, too60 segundos:

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a>toomodify Olá metadados de um conjunto de registro existente

[Metadados de conjunto de registros](dns-zones-records.md#tags-and-metadata) podem ser dados específicos do aplicativo de tooassociate usado com cada conjunto de registros, como pares chave-valor. Definir toomodify Olá metadados de um registro existente, use `azure network dns record-set set`. Para obter ajuda, consulte `azure network dns record-set set -h`.

Olá exemplo a seguir mostra como toomodify um conjunto de registros com duas entradas de metadados, "dept = Finanças" e "ambiente = produção", usando Olá `--metadata` parâmetro (forma abreviada `-m`). Observe que os metadados existentes são *substituído* pelos valores hello fornecidos.

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a>Excluir um conjunto de registros

Conjuntos de registros podem ser excluídos usando Olá `azure network dns record-set delete` comando. Para obter ajuda, consulte `azure network dns record-set delete -h`. Excluir um conjunto de registros também exclui todos os registros no conjunto de registros de saudação.

> [!NOTE]
> Você não pode excluir Olá SOA e NS conjuntos de registros no ápice da zona de saudação (`-Name "@"`).  Eles são criados automaticamente quando Olá zona foi criado e são excluídos automaticamente quando Olá zona é excluída.

Olá, exemplo a seguir exclui conjunto nomeado de registros de saudação *www* de um tipo de zona Olá *contoso.com* no grupo de recursos *MyResourceGroup*:

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

Você está operação de exclusão de saudação tooconfirm solicitada. toosuppress nesse prompt, use Olá `--quiet` alternar (forma abreviada `-q`).

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre as [zonas e os registros no DNS do Azure](dns-zones-records.md).
<br>
Saiba como muito[proteger suas zonas e registros de](dns-protect-zones-recordsets.md) ao usar o DNS do Azure.
