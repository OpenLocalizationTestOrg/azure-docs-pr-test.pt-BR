---
title: "aaaRed Hat atualização de infraestrutura (RHUI) | Microsoft Docs"
description: "Saiba mais sobre a Infraestrutura de Atualização do Red Hat (RHUI) para as instâncias sob demanda do Red Hat Enterprise Linux no Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: BorisB2015
manager: timlt
editor: 
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: cc244857104b25e4e61862c518db77e915e137ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a>Infraestrutura de Atualização do Red Hat (RHUI) para as VMs do Red Hat Enterprise Linux sob demanda no Azure
Máquinas virtuais criadas de saudação sob demanda Red Hat Enterprise Linux (RHEL) imagens disponíveis no Azure Marketplace são registrados tooaccess Olá infraestrutura de atualização da Hat (RHUI) da Red implantado no Azure.  instâncias RHEL sob demanda Olá tem repositório do acesso tooa yum regional e atualizações incrementais tooreceive capaz de.

lista de repositórios de yum Hello, que é gerenciada pelo RHUI, é configurada em sua instância do RHEL durante o provisionamento. Você não precisa toodo qualquer configuração adicional - executar `yum update` após a sua instância RHEL atualizações mais recentes do hello tooget pronto.

> [!NOTE]
> Setembro de 2016 implantamos um RHUI atualizada do Azure e em janeiro de 2017 começamos desligamento em fases de saudação RHUI mais antigas do Azure. Se você tiver sido usar imagens RHEL hello (ou seus instantâneos) de setembro de 2016 ou posterior - provavelmente nenhuma ação é necessária. Se, no entanto, você tiver instantâneos antigas/VMs, sua configuração deve toobe atualizado para acesso ininterrupto toohello RHUI do Azure.
> 

## <a name="rhui-azure-infrastructure-update"></a>Atualização da infraestrutura RHUI do Azure
A partir de setembro de 2016, o Azure tem um novo conjunto de servidores do RHUI (Red Hat Update Infrastructure). Esses servidores são implantados com o [Gerenciador de Tráfego do Azure](https://azure.microsoft.com/services/traffic-manager/) para que um único ponto de extremidade (rhui-1.microsoft.com) possa ser usado por qualquer VM, independentemente da região. Olá novas imagens de pré-pago RHEL (PAYG) hello Azure Marketplace (versões de setembro de 2016 ou posteriores) toohello ponto novos Azure RHUI servidores e não exigem nenhuma ação adicional.

### <a name="determine-if-action-is-required"></a>Determinar se uma ação é necessária
Se você estiver tendo problemas para se conectar tooAzure RHUI de sua VM do Azure RHEL PAYG, siga estas etapas
1. Inspecionar a configuração da VM para o ponto de extremidade do RHUI do Azure

    Verifique se `/etc/yum.repos.d/rh-cloud.repo` arquivo também contém referência`rhui-[1-3].microsoft.com` em baseurl de `[rhui-microsoft-azure-rhel*]` seção do arquivo hello. Se ele for, você está usando Olá RHUI nova do Azure.

    Se ele apontando tooa local com saudação padrão a seguir `mirrorlist.*cds[1-4].cloudapp.net` -Olá atualização de configuração é necessária.

    Se você estiver usando a nova configuração de saudação e ainda não puder conectar tooAzure RHUI - arquivo um caso de suporte com a Microsoft ou Red Hat.

    > [!NOTE]
    > Acesso hospedado tooAzure RHUI é limitado toohello VMs em [intervalos de IP de Datacenter do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).
    > 

2. Se hello RHUI antigo do Azure ainda estará disponível quando você fazer isso, verifique e você deseja que a configuração de saudação do tooautomatically atualização, execute Olá comando a seguir:

    `sudo yum update RHEL6`ou `sudo yum update RHEL7` dependendo da versão do hello RHEL família de produtos.

3. Se você não pode se conectar toohello RHUI antigo do Azure, siga Olá manual as etapas descritas na próxima seção, Olá.

4. Certifique-se de tooupdate configuração Olá Olá fonte/instantâneo de imagem afetados VM foi provisionado de.

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a>Desligamento em fases de Olá RHUI antigo do Azure
Durante o desligamento de saudação do hello antigo RHUI do Azure é restringir acesso tooit da seguinte maneira:

1. Restringir ainda mais tooset de acesso (ACL) de endereços IP que já estiverem se conectando tooit. Possíveis efeitos colaterais: se você continuar a usar Olá RHUI antigo do Azure - suas novas VMs podem não ser capaz de tooconnect tooit. RHEL VMs com IPs dinâmicos que passam por sequência de desligamento/desalocar/Iniciar pode receber o novo IP e, portanto, também pode começar a falhar tooconnect toohello RHUI antigo do Azure

2. Desligamento dos servidores de distribuição de conteúdo de espelho. Possíveis efeitos colaterais: como podemos desligar CDSes mais você pode ver mais `yum update` tempo de manutenção, tempos limite mais até Olá ponto quando você não pode se conectar toohello RHUI antigo do Azure.

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a>Olá IPs para novos servidores de fornecimento de conteúdo RHUI Olá são
Se você estiver usando toofurther de configuração de rede restringir o acesso de VMs de PAYG RHEL, certifique-se de saudação IPs a seguir é permitida para `yum update` toowork dependendo do ambiente Olá estão em. 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a>Atualização manual procedimento toouse Olá novo Azure RHUI servidores
Assinatura de chave pública do download (via ondulação) Olá

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

Verifique se a chave Olá baixado

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

Verifique a saída de hello, verifique se `keyid` e `user ID packet`:

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

Instalar a chave pública Olá

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

Baixar, verificar e instalar o cliente RPM

Download: para RHEL 6

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

Para RHEL 7

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

Verificar:

```bash
rpm -Kv azureclient.rpm
```

Verifique na saída de assinatura de saudação pacote é Okey

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

Instalar o RPM de saudação

```bash
sudo rpm -U azureclient.rpm
```

Após a conclusão, verifique se que você pode acessar saudação de forma RHUI Azure VM

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a>Em um script para automatizar a saudação anterior da tarefa
Use Olá script a seguir como tarefa de saudação tooautomate necessárias de atualização de VMs toohello novo Azure RHUI servidores afetados.

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a>Visão geral de RHUI
[Infraestrutura de atualização do Red Hat](https://access.redhat.com/products/red-hat-update-infrastructure) oferece o conteúdo do repositório uma solução altamente escalonável toomanage yum para instâncias de nuvem do Red Hat Enterprise Linux que são hospedadas por provedores de nuvem certificados com o Red Hat. Com base no projeto de pasta upstream hello, RHUI permite que provedores de nuvem toolocally espelho hospedado Red Hat repositório conteúdo, criar repositórios personalizados com seus próprios conteúdos e tornar esses repositórios disponíveis tooa grande grupo de usuários finais por meio de um balanceamento de carga sistema de entrega de conteúdo.

## <a name="regions-where-rhui-is-available"></a>Regiões em que o RHUI está disponível
O RHUI está disponível em todas as regiões onde as imagens do RHEL sob demanda estão disponíveis. Inclui todos os públicos regiões listadas em Olá atualmente [painel de status do Azure](https://azure.microsoft.com/status/) página regiões Azure US Government e Azure Alemanha. O acesso do RHUI para as VMs provisionadas a partir das imagens do RHEL sob demanda está incluído em seu preço. Disponibilidade de nuvem nacionais/regionais adicionais será atualizada à medida que expanda disponibilidade sob demanda RHEL Olá futuras.

> [!NOTE]
> Acesso hospedado tooAzure RHUI é limitado toohello VMs em [intervalos de IP de Datacenter do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

## <a name="get-updates-from-another-update-repository"></a>Obter atualizações de outro repositório de atualizações
Se você precisar tooget atualizações de um repositório de atualização diferentes (em vez de RHUI hospedado do Azure), primeiro é necessário toounregister suas instâncias de RHUI. Em seguida, você precisa registrar toore-los com a infraestrutura de atualização desejado hello (como Red Hat satélite ou Red Hat Customer Portal CDN). Você precisará das devidas assinaturas do Red Hat para esses serviços e o registro para o [Acesso em Nuvem da Red Hat no Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).

toounregister RHUI e registre novamente tooyour atualização infraestrutura siga estas etapas:

1. Editar /etc/yum.repos.d/rh-cloud.repo e altere todos os `enabled=1` muito`enabled=0`. Por exemplo:
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. Editar /etc/yum/pluginconf.d/rhnplugin.conf e alterar `enabled=0` muito`enabled=1`.
3. Em seguida, registre com a infraestrutura de saudação desejado, como o Portal do cliente Red Hat. Siga o guia de solução do Red Hat [como tooregister e assinar um toohello sistema Portal do cliente Red Hat](https://access.redhat.com/solutions/253273).

> [!NOTE]
> Acesso toohello RHUI hospedado do Azure está incluído no preço de imagem pré-pago RHEL (PAYG) hello. Cancelar o registro de uma VM do RHEL PAYG da saudação RHUI hospedado do Azure não converter máquina virtual de saudação em VM do tipo de trazer seu-proprietário-licença (BYOL). Se você registrar Olá mesma VM com outra fonte de atualizações pode incorrer encargos duplos: primeira vez para taxa de software Azure RHEL e hello pela segunda vez para Red Hat assinatura (s). 
> 
> Se você precisar consistentemente toouse uma infraestrutura de atualização que não seja hospedado no Azure RHUI considere a possibilidade de criar e implantar suas próprias imagens (tipo de BYOL), conforme descrito em [criar e carregar Red Hat com base em máquina virtual do Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artigo.
> 

## <a name="next-steps"></a>Próximas etapas
toocreate uma VM do Linux Red Hat Enterprise de imagem pré-pago do Azure Marketplace e aproveite hospedado no Azure RHUI ir muito[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/). Você será capaz de toouse `yum update` em sua instância RHEL sem qualquer configuração adicional.

