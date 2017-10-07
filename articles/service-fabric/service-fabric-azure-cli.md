---
title: "Introdução ao Azure Service Fabric XPlat CLI de aaaGetting"
description: "Introdução à CLI XPlat do Azure Service Fabric"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a><span data-ttu-id="b4081-103">Usando Olá XPlat CLI toointeract com um cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b4081-103">Using hello XPlat CLI toointeract with a Service Fabric cluster</span></span>

<span data-ttu-id="b4081-104">Você pode interagir com o cluster do Service Fabric máquinas Linux usando Olá XPlat CLI no Linux.</span><span class="sxs-lookup"><span data-stu-id="b4081-104">You can interact with Service Fabric cluster from Linux machines using hello XPlat CLI on Linux.</span></span>

<span data-ttu-id="b4081-105">primeira etapa de saudação é obter última versão Olá Olá CLI do representante de git hello e defina-o no seu caminho usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4081-105">hello first step is get hello latest version of hello CLI from hello git rep and set it up in your path using hello following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="b4081-106">Para cada comando, ele oferece suporte, você pode digitar o nome de saudação de ajuda de Olá Olá comando tooobtain para esse comando.</span><span class="sxs-lookup"><span data-stu-id="b4081-106">For each command, it supports, you can type hello name of hello command tooobtain hello help for that command.</span></span>
<span data-ttu-id="b4081-107">AutoCompletar tem suporte para comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4081-107">Auto-completion is supported for hello commands.</span></span> <span data-ttu-id="b4081-108">Por exemplo, hello fornece comando Ajuda para todos os comandos de aplicativo hello a seguir.</span><span class="sxs-lookup"><span data-stu-id="b4081-108">For example, hello following command gives you help for all hello application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="b4081-109">Você pode filtrar Olá ajuda tooa comando específico como Olá mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4081-109">You can further filter hello help tooa specific command, as hello following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="b4081-110">tooenable preenchimento automático no hello CLI, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4081-110">tooenable auto-completion in hello CLI, run hello following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="b4081-111">Olá comandos a seguir se conectar a cluster toohello e mostrar Olá nós no cluster de saudação:</span><span class="sxs-lookup"><span data-stu-id="b4081-111">hello following commands connect toohello cluster and show you hello nodes in hello cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="b4081-112">toouse parâmetros nomeados e localizar o que são, você pode digitar – ajuda após um comando.</span><span class="sxs-lookup"><span data-stu-id="b4081-112">toouse named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="b4081-113">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b4081-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="b4081-114">Ao conectar-se o cluster de vários computadores tooa de uma máquina **que não faça parte de cluster Olá**, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4081-114">When connecting tooa multi-machine cluster from a machine **that is not part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="b4081-115">Substitua marca de PublicIPorFQDN Olá com IP real hello ou FQDN conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="b4081-115">Replace hello PublicIPorFQDN tag with hello real IP or FQDN as appropriate.</span></span> <span data-ttu-id="b4081-116">Ao conectar-se o cluster de vários computadores tooa de uma máquina **que faz parte do cluster Olá**, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4081-116">When connecting tooa multi-machine cluster from a machine **that is part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="b4081-117">Você pode usar o PowerShell ou CLI toointeract com o Cluster de malha do serviço de Linux criadas por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4081-117">You can use PowerShell or CLI toointeract with your Linux Service Fabric Cluster created through hello Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="b4081-118">Esses agrupamentos não são seguros, assim, você pode abrir a caixa de um adicionando o endereço IP público de saudação no manifesto do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b4081-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding hello public IP address in hello cluster manifest.</span></span>

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a><span data-ttu-id="b4081-119">Usando Olá cluster do Service Fabric do XPlat CLI tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="b4081-119">Using hello XPlat CLI tooconnect tooa Service Fabric cluster</span></span>

<span data-ttu-id="b4081-120">Olá comandos de CLI do Azure a seguir descreve como tooconnect tooa proteger o cluster.</span><span class="sxs-lookup"><span data-stu-id="b4081-120">hello following Azure CLI commands describe how tooconnect tooa secure cluster.</span></span> <span data-ttu-id="b4081-121">detalhes do certificado Olá devem corresponder a um certificado em nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4081-121">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="b4081-122">Se seu certificado tem autoridades de certificação (CAs), será necessário tooadd Olá - AC-cert-path parâmetro, como Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4081-122">If your certificate has Certificate Authorities (CAs), you need tooadd hello --ca-cert-path parameter like hello following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="b4081-123">Se você tiver várias autoridades de certificação, use uma vírgula como delimitador hello.</span><span class="sxs-lookup"><span data-stu-id="b4081-123">If you have multiple CAs, use a comma as hello delimiter.</span></span>

<span data-ttu-id="b4081-124">Se seu nome comum no certificado de saudação não coincide com o ponto de extremidade de conexão de saudação, você pode usar o parâmetro hello `--strict-ssl-false` toobypass Olá verificação, conforme mostrado no hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4081-124">If your Common Name in hello certificate does not match hello connection endpoint, you could use hello parameter `--strict-ssl-false` toobypass hello verification as shown in hello following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="b4081-125">Se você quiser tooskip verificação de saudação da autoridade de certificação, você pode adicionar hello – parâmetro false não autorizado rejeitar conforme mostrado no comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="b4081-125">If you would like tooskip hello CA verification, you could add hello --reject-unauthorized-false parameter as shown in hello following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="b4081-126">Depois de se conectar, você deve ser capaz de toorun outros toointeract de comandos CLI com cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b4081-126">After you connect, you should be able toorun other CLI commands toointeract with hello cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="b4081-127">Implantando o aplicativo da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="b4081-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="b4081-128">Execute Olá comandos toocopy, registrar e iniciar o aplicativo de malha do serviço hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4081-128">Execute hello following commands toocopy, register, and start hello service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="b4081-129">Atualizando seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="b4081-129">Upgrading your application</span></span>

<span data-ttu-id="b4081-130">processo de saudação é semelhante toohello [processo no Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span><span class="sxs-lookup"><span data-stu-id="b4081-130">hello process is similar toohello [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="b4081-131">Crie, copie, registre e crie seu aplicativo por meio de um diretório raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="b4081-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="b4081-132">Se a instância do aplicativo é denominada `fabric:/MySFApp`e o tipo de saudação é MySFApp, comandos Olá seria o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b4081-132">If your application instance is named `fabric:/MySFApp`, and hello type is MySFApp, hello commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="b4081-133">Tornar Olá tooyour aplicação de alterações e recriar o serviço Olá modificado.</span><span class="sxs-lookup"><span data-stu-id="b4081-133">Make hello change tooyour application and rebuild hello modified service.</span></span>  <span data-ttu-id="b4081-134">Saudação de atualização modificada arquivo de manifesto do serviço (ServiceManifest.xml) com as versões atualizada de saudação para Olá serviço (e código ou configuração de dados conforme apropriado).</span><span class="sxs-lookup"><span data-stu-id="b4081-134">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="b4081-135">Também modificar o manifesto do aplicativo hello (ApplicationManifest.xml) com número de versão de hello atualizado para o aplicativo hello e Olá serviço modificado.</span><span class="sxs-lookup"><span data-stu-id="b4081-135">Also modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application, and hello modified service.</span></span>  <span data-ttu-id="b4081-136">Agora, copiar e registrar seu aplicativo atualizado usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4081-136">Now, copy and register your updated application using hello following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="b4081-137">Agora, você pode iniciar a atualização do aplicativo hello com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4081-137">Now, you can start hello application upgrade with hello following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="b4081-138">Agora você pode monitorar a atualização do aplicativo hello usando SFX.</span><span class="sxs-lookup"><span data-stu-id="b4081-138">You can now monitor hello application upgrade using SFX.</span></span> <span data-ttu-id="b4081-139">Em alguns minutos, aplicativo hello seria foram atualizado.</span><span class="sxs-lookup"><span data-stu-id="b4081-139">In a few minutes, hello application would have been updated.</span></span> <span data-ttu-id="b4081-140">Também pode tentar um aplicativo atualizado com um erro e verifique a funcionalidade de reversão automática Olá na malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="b4081-140">You can also try an updated app with an error and check hello auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-toopem-and-vice-versa"></a><span data-ttu-id="b4081-141">Convertendo do PFX tooPEM e vice-versa</span><span class="sxs-lookup"><span data-stu-id="b4081-141">Converting from PFX tooPEM and vice versa</span></span>

<span data-ttu-id="b4081-142">Talvez seja necessário um certificado de tooinstall dos clusters segura de tooaccess do computador local (com o Windows ou Linux) pode estar em um ambiente diferente.</span><span class="sxs-lookup"><span data-stu-id="b4081-142">You might need tooinstall a certificate in your local machine (with Windows or Linux) tooaccess secure clusters that may be in a different environment.</span></span> <span data-ttu-id="b4081-143">Por exemplo, ao acessar um cluster Linux protegido de um computador Windows e vice-versa talvez seja necessário tooconvert seu certificado de PFX tooPEM e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="b4081-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need tooconvert your certificate from PFX tooPEM and vice versa.</span></span> 

<span data-ttu-id="b4081-144">tooconvert de um PEM tooa arquivo PFX, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4081-144">tooconvert from a PEM file tooa PFX file, use hello following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="b4081-145">tooconvert de um arquivo PEM de tooa do arquivo PFX, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4081-145">tooconvert from a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="b4081-146">Consulte também[OpenSSL documentação](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="b4081-146">Refer too[OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="b4081-147">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="b4081-147">Troubleshooting</span></span>


### <a name="copying-of-hello-application-package-does-not-succeed"></a><span data-ttu-id="b4081-148">A cópia do pacote de aplicativo hello não for bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="b4081-148">Copying of hello application package does not succeed</span></span>

<span data-ttu-id="b4081-149">Verifique se `openssh` está instalado.</span><span class="sxs-lookup"><span data-stu-id="b4081-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="b4081-150">Por padrão, a área de trabalho do Ubuntu não está instalada.</span><span class="sxs-lookup"><span data-stu-id="b4081-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="b4081-151">Instale-o usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4081-151">Install it using hello following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="b4081-152">Se Olá problema persistir, tente desabilitar PAM para ssh alterando Olá `sshd_config` arquivo usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4081-152">If hello problem persists, try disabling PAM for ssh by changing hello `sshd_config` file using hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="b4081-153">Se Olá problema ainda persistir, tente número crescente de saudação do ssh sessões executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4081-153">If hello problem still persists, try increasing hello number of ssh sessions by executing hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="b4081-154">Usando chaves de ssh autenticação (como toopasswords contrário) ainda não tem suporte (como plataforma Olá usa ssh pacotes toocopy), para usar a autenticação de senha.</span><span class="sxs-lookup"><span data-stu-id="b4081-154">Using keys for ssh authentication (as opposed toopasswords) isn't yet supported (since hello platform uses ssh toocopy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4081-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b4081-155">Next steps</span></span>

[<span data-ttu-id="b4081-156">Configurar o ambiente de desenvolvimento hello e implantar um cluster do Service Fabric application tooa Linux.</span><span class="sxs-lookup"><span data-stu-id="b4081-156">Set up hello development environment and deploy a Service Fabric application tooa Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="b4081-157">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="b4081-157">Related articles</span></span>

* [<span data-ttu-id="b4081-158">Introdução ao Service Fabric e à CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="b4081-158">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
