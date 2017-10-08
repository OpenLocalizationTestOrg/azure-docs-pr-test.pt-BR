---
title: "gerenciamento de serviços de saudação do aaaHow toouse API (Python) - guia do recurso"
description: "Saiba como tooprogrammatically executar tarefas comuns de gerenciamento de serviço do Python."
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: b59622203470e1586484cec4033515edb39ca4d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-management-from-python"></a>Como toouse gerenciamento de serviço do Python
Este guia mostra como tooprogrammatically executar tarefas comuns de gerenciamento de serviço do Python. Olá **ServiceManagementService** classe Olá [Azure SDK para Python](https://github.com/Azure/azure-sdk-for-python) oferece suporte a acesso programático toomuch Olá relacionadas ao gerenciamento da funcionalidade do serviço que está disponível no hello [Portal clássico do azure] [ management-portal] (como **criar, atualizar e excluir serviços de nuvem e máquinas virtuais, serviços de gerenciamento de dados e implantações**). Essa funcionalidade pode ser útil na criação de aplicativos que precisam de gerenciamento de acesso programático à tooservice.

## <a name="WhatIs"> </a>O que é gerenciamento de serviços
Olá API de gerenciamento de serviço fornece acesso programático toomuch da funcionalidade de gerenciamento de serviços de saudação disponível por meio de saudação [portal clássico do Azure][management-portal]. Hello Azure SDK para Python permite toomanage seus serviços de nuvem e contas de armazenamento.

API de gerenciamento de serviços do toouse Olá, é necessário muito[criar uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="Concepts"> </a>Conceitos
Hello Azure SDK para Python encapsula Olá [API de gerenciamento de serviços do Azure][svc-mgmt-rest-api], que é uma API REST. Todas as operações da API são executadas por meio do SSL e mutuamente autenticadas usando certificados X.509 v3. serviço de gerenciamento de saudação pode ser acessado de dentro de um serviço em execução no Azure, ou diretamente na Internet de saudação de qualquer aplicativo que possa enviar uma solicitação HTTPS e receber uma resposta de HTTPS.

## <a name="Installation"> </a>Instalação
Todos os recursos de saudação descritos neste artigo estão disponíveis em Olá `azure-servicemanagement-legacy` pacote, que pode ser instalado usando o pip. Para obter mais informações sobre a instalação (por exemplo, se você for novo tooPython), consulte este artigo: [instalando Python e hello SDK do Azure](../python-how-to-install.md)

## <a name="Connect"></a>Como: conectar-se gerenciamento tooservice
ponto de extremidade de tooconnect toohello gerenciamento de serviço, você precisa sua ID de assinatura do Azure e um certificado de gerenciamento válido. Você pode obter sua ID de assinatura por meio de saudação [portal clássico do Azure][management-portal].

> [!NOTE]
> Agora é possível toouse certificados criados com OpenSSL quando em execução no Windows.  Isso requer o Python 2.7.4 ou posterior. É recomendável usuários toouse OpenSSL em vez de. pfx, já que o suporte para o. pfx certificados provavelmente serão removidos no futuro hello.
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a>Certificados de gerenciamento no Windows/Mac/Linux (OpenSSL)
Você pode usar [OpenSSL](http://www.openssl.org/) toocreate seu certificado de gerenciamento.  Você precisa realmente toocreate dois certificados, um servidor de saudação (uma `.cer` arquivo) e outro para o cliente da saudação (um `.pem` arquivo). Olá toocreate `.pem` de arquivos, execute:

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

Olá toocreate `.cer` do certificado, execute:

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

Para saber mais sobre certificados do Azure, confira [Visão geral dos Certificados de Serviços de Nuvem do Azure](cloud-services-certs-create.md). Para obter uma descrição completa dos parâmetros do OpenSSL, consulte a documentação de saudação em [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).

Depois de criar esses arquivos, você precisa Olá tooupload `.cer` tooAzure por meio de ação do hello "Carregar" do guia de "Configurações" hello de saudação do arquivo [portal clássico do Azure][management-portal], e você precisa toomake Anote onde você salvou Olá `.pem` arquivo.

Depois de obter sua ID de assinatura, um certificado criado e carregado Olá `.cer` tooAzure de arquivo, você pode conectar o ponto de extremidade de gerenciamento do Azure toohello, passando a id da assinatura hello e Olá caminho toohello `.pem` arquivo muito**ServiceManagementService**:

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

Em Olá anterior como exemplo, `sms` é um **ServiceManagementService** objeto. Olá **ServiceManagementService** classe é Olá classe primária usada toomanage serviços do Azure.

### <a name="management-certificates-on-windows-makecert"></a>Certificados de gerenciamento no Windows (MakeCert)
Você pode criar um certificado de gerenciamento autoassinado em seu computador usando `makecert.exe`.  Abra um **prompt de comando do Visual Studio** como um **administrador** e usar Olá comando a seguir, substituindo *AzureCertificate* com o nome do certificado Olá você gostaria que toouse.

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

comando Olá cria Olá `.cer` de arquivo e instala-o no hello **pessoal** repositório de certificados. Para obter mais informações, confira a [Visão geral sobre certificados para os Serviços de Nuvem do Azure](cloud-services-certs-create.md).

Depois de criar o certificado de saudação, você precisa Olá tooupload `.cer` tooAzure por meio de ação do hello "Carregar" do guia de "Configurações" hello de saudação do arquivo [portal clássico do Azure][management-portal].

Depois de obter sua ID de assinatura, um certificado criado e carregado Olá `.cer` tooAzure de arquivo, você pode conectar o ponto de extremidade de gerenciamento do Azure toohello, passando a id da assinatura hello e local de saudação do certificado de saudação em seu **Pessoal** repositório de certificados muito**ServiceManagementService** (novamente, substitua *AzureCertificate* com nome de saudação do certificado):

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

Em Olá anterior como exemplo, `sms` é um **ServiceManagementService** objeto. Olá **ServiceManagementService** classe é Olá classe primária usada toomanage serviços do Azure.

## <a name="ListAvailableLocations"> </a>Como listar os locais disponíveis
locais de saudação toolist que estão disponíveis para hospedar os serviços, use Olá **lista\_locais** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

Quando você criar um serviço de nuvem ou o serviço de armazenamento é necessário tooprovide um local válido. Olá **lista\_locais** método sempre retorna uma lista de locais disponíveis no momento da saudação atualizada. Redação deste artigo, locais de saudação disponíveis são:

* Europa Ocidental
* Norte da Europa
* Sudeste Asiático
* Ásia Oriental
* Centro dos EUA
* Centro-Norte dos EUA
* Centro-Sul dos Estados Unidos
* Oeste dos EUA
* Leste dos EUA
* Leste do Japão
* Oeste do Japão
* Sul do Brasil
* Leste da Austrália
* Sudeste da Austrália

## <a name="CreateCloudService"> </a>Como criar um serviço de nuvem
Quando você cria um aplicativo e executá-lo no Azure, código de saudação e configuração junto são chamados de um Azure [serviço de nuvem] [ cloud service] (conhecido como um *serviço hospedado* no anterior Versões do Azure). Olá **criar\_hospedado\_service** método permite toocreate um novo serviço hospedado, fornecendo um nome de serviço hospedado (que deve ser exclusivo no Azure), um rótulo (toobase64 automaticamente codificado), um Descrição e um local.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

Você pode listar todos os serviços de saudação hospedado para sua assinatura com hello **lista\_hospedado\_serviços** método:

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

Se você quiser tooget informações sobre um serviço hospedado em particular, você pode fazer isso passando toohello de nome de serviço hospedada de saudação **obter\_hospedado\_service\_propriedades** método:

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

Depois de criar um serviço de nuvem, você pode implantar o serviço de toohello de código com hello **criar\_implantação** método.

## <a name="DeleteCloudService"> </a>Como excluir um serviço de nuvem
Você pode excluir um serviço de nuvem passando Olá serviço nome toohello **excluir\_hospedado\_service** método:

    sms.delete_hosted_service('myhostedservice')

Antes de excluir um serviço, todas as implantações de serviço Olá devem ser excluídas primeiro. (Consulte [Como excluir uma implantação](#DeleteDeployment) para obter detalhes.)

## <a name="DeleteDeployment"> </a>Como excluir uma implantação
toodelete uma implantação, use Olá **excluir\_implantação** método. Olá exemplo a seguir mostra como toodelete uma implantação denominada `v1`.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <a name="CreateStorageService"> </a>Como criar um serviço de armazenamento
Um [serviço de armazenamento](../storage/common/storage-create-storage-account.md) oferece acesso tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tabelas](../cosmos-db/table-storage-how-to-use-python.md), e [filas](../storage/queues/storage-python-how-to-use-queue-storage.md). toocreate um serviço de armazenamento, é necessário um nome para o serviço de saudação (entre 3 e 24 caracteres minúsculos e exclusivo dentro do Azure), uma descrição, um rótulo (backup too100 caracteres, toobase64 automaticamente codificada) e um local. saudação de exemplo a seguir mostra como toocreate um armazenamento de serviço especificando um local.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

Observe que esse status de saudação do hello no Olá anterior exemplo **criar\_armazenamento\_conta** operação pode ser recuperada, passando o resultado de saudação retornado por **criar\_armazenamento \_conta** toohello **obter\_operação\_status** método.  

Você pode listar suas contas de armazenamento e suas propriedades com hello **lista\_armazenamento\_contas** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <a name="DeleteStorageService"> </a>Como excluir um serviço de armazenamento
Você pode excluir um serviço de armazenamento, passando toohello de nome de serviço de armazenamento de saudação **excluir\_armazenamento\_conta** método. A exclusão de um serviço de armazenamento exclui todos os dados armazenados no serviço de saudação (blobs, tabelas e filas).

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <a name="ListOperatingSystems"> </a>Como listar os sistemas operacionais disponíveis
toolist Olá os sistemas operacionais que estão disponíveis para hospedar os serviços, usam Olá **lista\_operacional\_sistemas** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

Como alternativa, você pode usar o hello **lista\_operacional\_sistema\_famílias** método, que agrupa os sistemas operacionais de saudação por família:

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <a name="CreateVMImage"> </a>Como criar uma imagem do sistema operacional
tooadd um repositório de imagens de toohello de imagem de sistema operacional, use Olá **adicionar\_os\_imagem** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

imagens do sistema operacional Olá toolist que estão disponíveis, use Olá **lista\_os\_imagens** método. Isso inclui todas as imagens de plataforma e imagens do usuário:

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <a name="DeleteVMImage"> </a>Como excluir uma imagem do sistema operacional
toodelete uma imagem do usuário, use Olá **excluir\_os\_imagem** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <a name="CreateVM"> </a>Como criar uma máquina virtual
toocreate uma máquina virtual, primeiro é necessário toocreate um [serviço de nuvem](#CreateCloudService).  Criar implantação da máquina virtual hello usando Olá **criar\_virtual\_máquina\_implantação** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where hello VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <a name="DeleteVM"> </a>Como excluir uma máquina virtual
toodelete uma máquina virtual, você primeiro excluir Olá implantação usando Olá **excluir\_implantação** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

serviço de nuvem Olá pode ser excluído usando Olá **excluir\_hospedado\_service** método:

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a>Como criar uma máquina virtual por meio de uma imagem de máquina virtual capturada
toocapture uma imagem de VM, você primeiro chamar hello **capturar\_vm\_imagem** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace hello below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

Em seguida, toomake-se de que você capturou com êxito a imagem hello, use Olá **lista\_vm\_imagens** api e certifique-se de sua imagem é exibida nos resultados da saudação:

    images = sms.list_vm_images()

toofinally criar máquina virtual de saudação usando a imagem capturada hello, use Olá **criar\_virtual\_máquina\_implantação** método como antes, mas desta vez passar Olá vm_image_name em vez disso

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

Saiba mais sobre toolearn como toocapture uma máquina Virtual Linux, consulte [como tooCapture uma máquina Virtual Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

Saiba mais sobre toolearn como toocapture uma máquina Virtual do Windows, consulte [como tooCapture uma máquina Virtual do Windows.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="What's Next"> </a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação do gerenciamento de serviços, você pode acessar Olá [documentação de referência de API completa para hello Azure SDK de Python](http://azure-sdk-for-python.readthedocs.org/) e executar complexo tarefas facilmente toomanage seu aplicativo de python.

Para obter mais informações, consulte Olá [Central de desenvolvedores de Python](/develop/python/).

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect tooservice management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
