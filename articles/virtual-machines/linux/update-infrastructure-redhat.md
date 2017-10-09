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
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="d655b-103">Infraestrutura de Atualização do Red Hat (RHUI) para as VMs do Red Hat Enterprise Linux sob demanda no Azure</span><span class="sxs-lookup"><span data-stu-id="d655b-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="d655b-104">Máquinas virtuais criadas de saudação sob demanda Red Hat Enterprise Linux (RHEL) imagens disponíveis no Azure Marketplace são registrados tooaccess Olá infraestrutura de atualização da Hat (RHUI) da Red implantado no Azure.</span><span class="sxs-lookup"><span data-stu-id="d655b-104">Virtual machines created from hello on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered tooaccess hello Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="d655b-105">instâncias RHEL sob demanda Olá tem repositório do acesso tooa yum regional e atualizações incrementais tooreceive capaz de.</span><span class="sxs-lookup"><span data-stu-id="d655b-105">hello on-demand RHEL instances have access tooa regional yum repository and able tooreceive incremental updates.</span></span>

<span data-ttu-id="d655b-106">lista de repositórios de yum Hello, que é gerenciada pelo RHUI, é configurada em sua instância do RHEL durante o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="d655b-106">hello yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="d655b-107">Você não precisa toodo qualquer configuração adicional - executar `yum update` após a sua instância RHEL atualizações mais recentes do hello tooget pronto.</span><span class="sxs-lookup"><span data-stu-id="d655b-107">You don't need toodo any additional configuration - run `yum update` after your RHEL instance is ready tooget hello latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="d655b-108">Setembro de 2016 implantamos um RHUI atualizada do Azure e em janeiro de 2017 começamos desligamento em fases de saudação RHUI mais antigas do Azure.</span><span class="sxs-lookup"><span data-stu-id="d655b-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of hello older Azure RHUI.</span></span> <span data-ttu-id="d655b-109">Se você tiver sido usar imagens RHEL hello (ou seus instantâneos) de setembro de 2016 ou posterior - provavelmente nenhuma ação é necessária.</span><span class="sxs-lookup"><span data-stu-id="d655b-109">If you have been using hello RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="d655b-110">Se, no entanto, você tiver instantâneos antigas/VMs, sua configuração deve toobe atualizado para acesso ininterrupto toohello RHUI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d655b-110">If, however, you have older snapshots/VMs, their configuration needs toobe updated for uninterrupted access toohello Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="d655b-111">Atualização da infraestrutura RHUI do Azure</span><span class="sxs-lookup"><span data-stu-id="d655b-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="d655b-112">A partir de setembro de 2016, o Azure tem um novo conjunto de servidores do RHUI (Red Hat Update Infrastructure).</span><span class="sxs-lookup"><span data-stu-id="d655b-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="d655b-113">Esses servidores são implantados com o [Gerenciador de Tráfego do Azure](https://azure.microsoft.com/services/traffic-manager/) para que um único ponto de extremidade (rhui-1.microsoft.com) possa ser usado por qualquer VM, independentemente da região.</span><span class="sxs-lookup"><span data-stu-id="d655b-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="d655b-114">Olá novas imagens de pré-pago RHEL (PAYG) hello Azure Marketplace (versões de setembro de 2016 ou posteriores) toohello ponto novos Azure RHUI servidores e não exigem nenhuma ação adicional.</span><span class="sxs-lookup"><span data-stu-id="d655b-114">hello new RHEL Pay-As-You-Go (PAYG) images in hello Azure Marketplace (versions dated September 2016 or later) point toohello new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="d655b-115">Determinar se uma ação é necessária</span><span class="sxs-lookup"><span data-stu-id="d655b-115">Determine if action is required</span></span>
<span data-ttu-id="d655b-116">Se você estiver tendo problemas para se conectar tooAzure RHUI de sua VM do Azure RHEL PAYG, siga estas etapas</span><span class="sxs-lookup"><span data-stu-id="d655b-116">If you are experiencing problems connecting tooAzure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="d655b-117">Inspecionar a configuração da VM para o ponto de extremidade do RHUI do Azure</span><span class="sxs-lookup"><span data-stu-id="d655b-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="d655b-118">Verifique se `/etc/yum.repos.d/rh-cloud.repo` arquivo também contém referência`rhui-[1-3].microsoft.com` em baseurl de `[rhui-microsoft-azure-rhel*]` seção do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="d655b-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference too`rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of hello file.</span></span> <span data-ttu-id="d655b-119">Se ele for, você está usando Olá RHUI nova do Azure.</span><span class="sxs-lookup"><span data-stu-id="d655b-119">If it is - you are using hello new Azure RHUI.</span></span>

    <span data-ttu-id="d655b-120">Se ele apontando tooa local com saudação padrão a seguir `mirrorlist.*cds[1-4].cloudapp.net` -Olá atualização de configuração é necessária.</span><span class="sxs-lookup"><span data-stu-id="d655b-120">If it pointing tooa location with hello following pattern `mirrorlist.*cds[1-4].cloudapp.net` - hello configuration update is required.</span></span>

    <span data-ttu-id="d655b-121">Se você estiver usando a nova configuração de saudação e ainda não puder conectar tooAzure RHUI - arquivo um caso de suporte com a Microsoft ou Red Hat.</span><span class="sxs-lookup"><span data-stu-id="d655b-121">If you are using hello new configuration and still cannot connect tooAzure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d655b-122">Acesso hospedado tooAzure RHUI é limitado toohello VMs em [intervalos de IP de Datacenter do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="d655b-122">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="d655b-123">Se hello RHUI antigo do Azure ainda estará disponível quando você fazer isso, verifique e você deseja que a configuração de saudação do tooautomatically atualização, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d655b-123">If hello old Azure RHUI is still available when you do this check and you would like tooautomatically update hello configuration, execute hello following command:</span></span>

    <span data-ttu-id="d655b-124">`sudo yum update RHEL6`ou `sudo yum update RHEL7` dependendo da versão do hello RHEL família de produtos.</span><span class="sxs-lookup"><span data-stu-id="d655b-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on hello RHEL family version.</span></span>

3. <span data-ttu-id="d655b-125">Se você não pode se conectar toohello RHUI antigo do Azure, siga Olá manual as etapas descritas na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="d655b-125">If you can no longer connect toohello old Azure RHUI, follow hello manual steps described in hello next section.</span></span>

4. <span data-ttu-id="d655b-126">Certifique-se de tooupdate configuração Olá Olá fonte/instantâneo de imagem afetados VM foi provisionado de.</span><span class="sxs-lookup"><span data-stu-id="d655b-126">Make sure tooupdate hello configuration on hello source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a><span data-ttu-id="d655b-127">Desligamento em fases de Olá RHUI antigo do Azure</span><span class="sxs-lookup"><span data-stu-id="d655b-127">Phased shutdown of hello old Azure RHUI</span></span>
<span data-ttu-id="d655b-128">Durante o desligamento de saudação do hello antigo RHUI do Azure é restringir acesso tooit da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d655b-128">During hello shutdown of hello old Azure RHUI we restrict access tooit as follows:</span></span>

1. <span data-ttu-id="d655b-129">Restringir ainda mais tooset de acesso (ACL) de endereços IP que já estiverem se conectando tooit.</span><span class="sxs-lookup"><span data-stu-id="d655b-129">Further restrict access (ACL) tooset of IP addresses that are already connecting tooit.</span></span> <span data-ttu-id="d655b-130">Possíveis efeitos colaterais: se você continuar a usar Olá RHUI antigo do Azure - suas novas VMs podem não ser capaz de tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="d655b-130">Possible side-effects: if you continue using hello old Azure RHUI - your new VMs may not be able tooconnect tooit.</span></span> <span data-ttu-id="d655b-131">RHEL VMs com IPs dinâmicos que passam por sequência de desligamento/desalocar/Iniciar pode receber o novo IP e, portanto, também pode começar a falhar tooconnect toohello RHUI antigo do Azure</span><span class="sxs-lookup"><span data-stu-id="d655b-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing tooconnect toohello old Azure RHUI</span></span>

2. <span data-ttu-id="d655b-132">Desligamento dos servidores de distribuição de conteúdo de espelho.</span><span class="sxs-lookup"><span data-stu-id="d655b-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="d655b-133">Possíveis efeitos colaterais: como podemos desligar CDSes mais você pode ver mais `yum update` tempo de manutenção, tempos limite mais até Olá ponto quando você não pode se conectar toohello RHUI antigo do Azure.</span><span class="sxs-lookup"><span data-stu-id="d655b-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until hello point when you can no longer connect toohello old Azure RHUI.</span></span>

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="d655b-134">Olá IPs para novos servidores de fornecimento de conteúdo RHUI Olá são</span><span class="sxs-lookup"><span data-stu-id="d655b-134">hello IPs for hello new RHUI content delivery servers are</span></span>
<span data-ttu-id="d655b-135">Se você estiver usando toofurther de configuração de rede restringir o acesso de VMs de PAYG RHEL, certifique-se de saudação IPs a seguir é permitida para `yum update` toowork dependendo do ambiente Olá estão em.</span><span class="sxs-lookup"><span data-stu-id="d655b-135">If you are using network configuration toofurther restrict access from RHEL PAYG VMs, make sure hello following IPs are allowed for `yum update` toowork depending on hello environment you are in.</span></span> 

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

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a><span data-ttu-id="d655b-136">Atualização manual procedimento toouse Olá novo Azure RHUI servidores</span><span class="sxs-lookup"><span data-stu-id="d655b-136">Manual update procedure toouse hello new Azure RHUI servers</span></span>
<span data-ttu-id="d655b-137">Assinatura de chave pública do download (via ondulação) Olá</span><span class="sxs-lookup"><span data-stu-id="d655b-137">Download (via curl) hello public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="d655b-138">Verifique se a chave Olá baixado</span><span class="sxs-lookup"><span data-stu-id="d655b-138">Verify hello downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="d655b-139">Verifique a saída de hello, verifique se `keyid` e `user ID packet`:</span><span class="sxs-lookup"><span data-stu-id="d655b-139">Check hello output, verify `keyid` and `user ID packet`:</span></span>

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

<span data-ttu-id="d655b-140">Instalar a chave pública Olá</span><span class="sxs-lookup"><span data-stu-id="d655b-140">Install hello public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="d655b-141">Baixar, verificar e instalar o cliente RPM</span><span class="sxs-lookup"><span data-stu-id="d655b-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="d655b-142">Download: para RHEL 6</span><span class="sxs-lookup"><span data-stu-id="d655b-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="d655b-143">Para RHEL 7</span><span class="sxs-lookup"><span data-stu-id="d655b-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="d655b-144">Verificar:</span><span class="sxs-lookup"><span data-stu-id="d655b-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="d655b-145">Verifique na saída de assinatura de saudação pacote é Okey</span><span class="sxs-lookup"><span data-stu-id="d655b-145">Check in output that signature of hello package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="d655b-146">Instalar o RPM de saudação</span><span class="sxs-lookup"><span data-stu-id="d655b-146">Install hello RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="d655b-147">Após a conclusão, verifique se que você pode acessar saudação de forma RHUI Azure VM</span><span class="sxs-lookup"><span data-stu-id="d655b-147">Upon completion, verify that you can access Azure RHUI form hello VM</span></span>

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a><span data-ttu-id="d655b-148">Em um script para automatizar a saudação anterior da tarefa</span><span class="sxs-lookup"><span data-stu-id="d655b-148">All-in-one script for automating hello preceding task</span></span>
<span data-ttu-id="d655b-149">Use Olá script a seguir como tarefa de saudação tooautomate necessárias de atualização de VMs toohello novo Azure RHUI servidores afetados.</span><span class="sxs-lookup"><span data-stu-id="d655b-149">Use hello following script as needed tooautomate hello task of updating affected VMs toohello new Azure RHUI servers.</span></span>

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

## <a name="rhui-overview"></a><span data-ttu-id="d655b-150">Visão geral de RHUI</span><span class="sxs-lookup"><span data-stu-id="d655b-150">RHUI overview</span></span>
<span data-ttu-id="d655b-151">[Infraestrutura de atualização do Red Hat](https://access.redhat.com/products/red-hat-update-infrastructure) oferece o conteúdo do repositório uma solução altamente escalonável toomanage yum para instâncias de nuvem do Red Hat Enterprise Linux que são hospedadas por provedores de nuvem certificados com o Red Hat.</span><span class="sxs-lookup"><span data-stu-id="d655b-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution toomanage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="d655b-152">Com base no projeto de pasta upstream hello, RHUI permite que provedores de nuvem toolocally espelho hospedado Red Hat repositório conteúdo, criar repositórios personalizados com seus próprios conteúdos e tornar esses repositórios disponíveis tooa grande grupo de usuários finais por meio de um balanceamento de carga sistema de entrega de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="d655b-152">Based on hello upstream Pulp project, RHUI allows cloud providers toolocally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available tooa large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="d655b-153">Regiões em que o RHUI está disponível</span><span class="sxs-lookup"><span data-stu-id="d655b-153">Regions where RHUI is available</span></span>
<span data-ttu-id="d655b-154">O RHUI está disponível em todas as regiões onde as imagens do RHEL sob demanda estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="d655b-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="d655b-155">Inclui todos os públicos regiões listadas em Olá atualmente [painel de status do Azure](https://azure.microsoft.com/status/) página regiões Azure US Government e Azure Alemanha.</span><span class="sxs-lookup"><span data-stu-id="d655b-155">It currently includes all public regions listed on hello [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="d655b-156">O acesso do RHUI para as VMs provisionadas a partir das imagens do RHEL sob demanda está incluído em seu preço.</span><span class="sxs-lookup"><span data-stu-id="d655b-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="d655b-157">Disponibilidade de nuvem nacionais/regionais adicionais será atualizada à medida que expanda disponibilidade sob demanda RHEL Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="d655b-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="d655b-158">Acesso hospedado tooAzure RHUI é limitado toohello VMs em [intervalos de IP de Datacenter do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="d655b-158">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="d655b-159">Obter atualizações de outro repositório de atualizações</span><span class="sxs-lookup"><span data-stu-id="d655b-159">Get updates from another update repository</span></span>
<span data-ttu-id="d655b-160">Se você precisar tooget atualizações de um repositório de atualização diferentes (em vez de RHUI hospedado do Azure), primeiro é necessário toounregister suas instâncias de RHUI.</span><span class="sxs-lookup"><span data-stu-id="d655b-160">If you need tooget updates from a different update repository (instead of Azure-hosted RHUI), first you need toounregister your instances from RHUI.</span></span> <span data-ttu-id="d655b-161">Em seguida, você precisa registrar toore-los com a infraestrutura de atualização desejado hello (como Red Hat satélite ou Red Hat Customer Portal CDN).</span><span class="sxs-lookup"><span data-stu-id="d655b-161">Then you need toore-register them with hello desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="d655b-162">Você precisará das devidas assinaturas do Red Hat para esses serviços e o registro para o [Acesso em Nuvem da Red Hat no Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="d655b-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="d655b-163">toounregister RHUI e registre novamente tooyour atualização infraestrutura siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="d655b-163">toounregister RHUI and reregister tooyour update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="d655b-164">Editar /etc/yum.repos.d/rh-cloud.repo e altere todos os `enabled=1` muito`enabled=0`.</span><span class="sxs-lookup"><span data-stu-id="d655b-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` too`enabled=0`.</span></span> <span data-ttu-id="d655b-165">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d655b-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="d655b-166">Editar /etc/yum/pluginconf.d/rhnplugin.conf e alterar `enabled=0` muito`enabled=1`.</span><span class="sxs-lookup"><span data-stu-id="d655b-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` too`enabled=1`.</span></span>
3. <span data-ttu-id="d655b-167">Em seguida, registre com a infraestrutura de saudação desejado, como o Portal do cliente Red Hat.</span><span class="sxs-lookup"><span data-stu-id="d655b-167">Then register with hello desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="d655b-168">Siga o guia de solução do Red Hat [como tooregister e assinar um toohello sistema Portal do cliente Red Hat](https://access.redhat.com/solutions/253273).</span><span class="sxs-lookup"><span data-stu-id="d655b-168">Follow Red Hat solution guide on [how tooregister and subscribe a system toohello Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="d655b-169">Acesso toohello RHUI hospedado do Azure está incluído no preço de imagem pré-pago RHEL (PAYG) hello.</span><span class="sxs-lookup"><span data-stu-id="d655b-169">Access toohello Azure-hosted RHUI is included in hello RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="d655b-170">Cancelar o registro de uma VM do RHEL PAYG da saudação RHUI hospedado do Azure não converter máquina virtual de saudação em VM do tipo de trazer seu-proprietário-licença (BYOL).</span><span class="sxs-lookup"><span data-stu-id="d655b-170">Unregistering a PAYG RHEL VM from hello Azure-hosted RHUI does not convert hello virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="d655b-171">Se você registrar Olá mesma VM com outra fonte de atualizações pode incorrer encargos duplos: primeira vez para taxa de software Azure RHEL e hello pela segunda vez para Red Hat assinatura (s).</span><span class="sxs-lookup"><span data-stu-id="d655b-171">If you register hello same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and hello second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="d655b-172">Se você precisar consistentemente toouse uma infraestrutura de atualização que não seja hospedado no Azure RHUI considere a possibilidade de criar e implantar suas próprias imagens (tipo de BYOL), conforme descrito em [criar e carregar Red Hat com base em máquina virtual do Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artigo.</span><span class="sxs-lookup"><span data-stu-id="d655b-172">If you consistently need toouse an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="d655b-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d655b-173">Next steps</span></span>
<span data-ttu-id="d655b-174">toocreate uma VM do Linux Red Hat Enterprise de imagem pré-pago do Azure Marketplace e aproveite hospedado no Azure RHUI ir muito[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span><span class="sxs-lookup"><span data-stu-id="d655b-174">toocreate a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="d655b-175">Você será capaz de toouse `yum update` em sua instância RHEL sem qualquer configuração adicional.</span><span class="sxs-lookup"><span data-stu-id="d655b-175">You will be able toouse `yum update` in your RHEL instance without any additional setup.</span></span>

