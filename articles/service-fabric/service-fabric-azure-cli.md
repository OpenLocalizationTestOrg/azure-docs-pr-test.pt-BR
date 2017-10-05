---
title: "Introdução à CLI XPlat do Azure Service Fabric"
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
ms.openlocfilehash: ddf881f6c202a82a3f64773639aa29b660057f8d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-xplat-cli-to-interact-with-a-service-fabric-cluster"></a><span data-ttu-id="3997c-103">Usando a CLI XPlat para interagir com um cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3997c-103">Using the XPlat CLI to interact with a Service Fabric cluster</span></span>

<span data-ttu-id="3997c-104">Você pode interagir com o cluster do Service Fabric por meio de computadores Linux usando a CLI XPlat no Linux.</span><span class="sxs-lookup"><span data-stu-id="3997c-104">You can interact with Service Fabric cluster from Linux machines using the XPlat CLI on Linux.</span></span>

<span data-ttu-id="3997c-105">A primeira etapa é obter a versão mais recente da CLI do representante de git e configurá-la em seu caminho usando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="3997c-105">The first step is get the latest version of the CLI from the git rep and set it up in your path using the following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="3997c-106">Para cada comando com suporte, você pode digitar o nome do comando para obter ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="3997c-106">For each command, it supports, you can type the name of the command to obtain the help for that command.</span></span>
<span data-ttu-id="3997c-107">Há suporte para o preenchimento automático para os comandos.</span><span class="sxs-lookup"><span data-stu-id="3997c-107">Auto-completion is supported for the commands.</span></span> <span data-ttu-id="3997c-108">Por exemplo, o comando a seguir fornece ajuda para todos os comandos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3997c-108">For example, the following command gives you help for all the application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="3997c-109">Você pode filtrar ainda mais a ajuda para um comando específico, como mostra o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="3997c-109">You can further filter the help to a specific command, as the following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="3997c-110">Para habilitar o preenchimento automático na CLI, execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="3997c-110">To enable auto-completion in the CLI, run the following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="3997c-111">Os comandos a seguir se conectam ao cluster e mostram os nós no cluster:</span><span class="sxs-lookup"><span data-stu-id="3997c-111">The following commands connect to the cluster and show you the nodes in the cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="3997c-112">Para usar parâmetros nomeados e descobrir o que eles são, você pode digitar -–ajuda após um comando.</span><span class="sxs-lookup"><span data-stu-id="3997c-112">To use named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="3997c-113">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3997c-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="3997c-114">Ao se conectar a um cluster com vários computadores por meio de um computador **que não faz parte do cluster**, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="3997c-114">When connecting to a multi-machine cluster from a machine **that is not part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="3997c-115">Substitua a marcação PublicIPorFQDN por um IP ou FQDN real, conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="3997c-115">Replace the PublicIPorFQDN tag with the real IP or FQDN as appropriate.</span></span> <span data-ttu-id="3997c-116">Ao se conectar a um cluster com vários computadores por meio de um computador **que faz parte do cluster**, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="3997c-116">When connecting to a multi-machine cluster from a machine **that is part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="3997c-117">Você pode usar o PowerShell ou a CLI para interagir com o Cluster do Service Fabric do Linux criado por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3997c-117">You can use PowerShell or CLI to interact with your Linux Service Fabric Cluster created through the Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="3997c-118">Esses clusters não são seguros, portanto, você pode estar se expondo ao adicionar o endereço IP público ao manifesto do cluster.</span><span class="sxs-lookup"><span data-stu-id="3997c-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding the public IP address in the cluster manifest.</span></span>

## <a name="using-the-xplat-cli-to-connect-to-a-service-fabric-cluster"></a><span data-ttu-id="3997c-119">Usando a CLI XPlat para se conectar a um cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3997c-119">Using the XPlat CLI to connect to a Service Fabric cluster</span></span>

<span data-ttu-id="3997c-120">Os seguintes comandos da CLI do Azure descrevem como se conectar a um cluster seguro.</span><span class="sxs-lookup"><span data-stu-id="3997c-120">The following Azure CLI commands describe how to connect to a secure cluster.</span></span> <span data-ttu-id="3997c-121">Os detalhes do certificado devem corresponder a um certificado em nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="3997c-121">The certificate details must match a certificate on the cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="3997c-122">Se o certificado tiver ACs (autoridades de certificação), você precisará adicionar o parâmetro --ca-cert-path, como no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="3997c-122">If your certificate has Certificate Authorities (CAs), you need to add the --ca-cert-path parameter like the following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="3997c-123">Se você tiver várias ACs, use uma vírgula como o delimitador.</span><span class="sxs-lookup"><span data-stu-id="3997c-123">If you have multiple CAs, use a comma as the delimiter.</span></span>

<span data-ttu-id="3997c-124">Se o Nome Comum no certificado não coincidir com o ponto de extremidade de conexão, você poderá usar o parâmetro `--strict-ssl-false` para ignorar a verificação, conforme mostrado no seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="3997c-124">If your Common Name in the certificate does not match the connection endpoint, you could use the parameter `--strict-ssl-false` to bypass the verification as shown in the following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="3997c-125">Se quiser ignorar a verificação de AC, você poderá adicionar o parâmetro --reject-unauthorized-false, conforme mostrado no seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="3997c-125">If you would like to skip the CA verification, you could add the --reject-unauthorized-false parameter as shown in the following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="3997c-126">Depois de se conectar, você poderá executar outros comandos da CLI para interagir com o cluster.</span><span class="sxs-lookup"><span data-stu-id="3997c-126">After you connect, you should be able to run other CLI commands to interact with the cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="3997c-127">Implantando o aplicativo da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="3997c-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="3997c-128">Execute os seguintes comandos para copiar, registrar e iniciar o aplicativo Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="3997c-128">Execute the following commands to copy, register, and start the service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="3997c-129">Atualizando seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="3997c-129">Upgrading your application</span></span>

<span data-ttu-id="3997c-130">O processo é semelhante ao [processo no Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span><span class="sxs-lookup"><span data-stu-id="3997c-130">The process is similar to the [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="3997c-131">Crie, copie, registre e crie seu aplicativo por meio de um diretório raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="3997c-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="3997c-132">Se a instância do aplicativo for denominada `fabric:/MySFApp` e o tipo for MySFApp, os comandos serão da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3997c-132">If your application instance is named `fabric:/MySFApp`, and the type is MySFApp, the commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="3997c-133">Faça a alteração em seu aplicativo e recompile o serviço modificado.</span><span class="sxs-lookup"><span data-stu-id="3997c-133">Make the change to your application and rebuild the modified service.</span></span>  <span data-ttu-id="3997c-134">Atualize o arquivo de manifesto do serviço modificado (ServiceManifest.xml) com as versões atualizadas para o Serviço (e Código, Configuração ou Dados, conforme apropriado).</span><span class="sxs-lookup"><span data-stu-id="3997c-134">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="3997c-135">Modifique também o manifesto do aplicativo (ApplicationManifest.xml) com o número da versão atualizada do aplicativo e o serviço modificado.</span><span class="sxs-lookup"><span data-stu-id="3997c-135">Also modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application, and the modified service.</span></span>  <span data-ttu-id="3997c-136">Agora, copie e registre seu aplicativo atualizado usando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="3997c-136">Now, copy and register your updated application using the following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="3997c-137">Agora, você pode iniciar a atualização de aplicativo com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="3997c-137">Now, you can start the application upgrade with the following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="3997c-138">Agora você pode monitorar a atualização de aplicativo usando SFX.</span><span class="sxs-lookup"><span data-stu-id="3997c-138">You can now monitor the application upgrade using SFX.</span></span> <span data-ttu-id="3997c-139">Em alguns minutos, o aplicativo seria atualizado.</span><span class="sxs-lookup"><span data-stu-id="3997c-139">In a few minutes, the application would have been updated.</span></span> <span data-ttu-id="3997c-140">Você também pode experimentar um aplicativo atualizado com um erro e verificar a funcionalidade de reversão automática no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3997c-140">You can also try an updated app with an error and check the auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-to-pem-and-vice-versa"></a><span data-ttu-id="3997c-141">Convertendo de PFX para PEM e vice-versa</span><span class="sxs-lookup"><span data-stu-id="3997c-141">Converting from PFX to PEM and vice versa</span></span>

<span data-ttu-id="3997c-142">Pode ser necessário instalar um certificado no seu computador local (com o Windows ou Linux) para acessar os clusters seguros que podem estar em um ambiente diferente.</span><span class="sxs-lookup"><span data-stu-id="3997c-142">You might need to install a certificate in your local machine (with Windows or Linux) to access secure clusters that may be in a different environment.</span></span> <span data-ttu-id="3997c-143">Por exemplo, ao acessar um cluster protegido do Linux de um computador Windows e vice-versa, pode ser necessário converter seu certificado de PFX para PEM e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="3997c-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need to convert your certificate from PFX to PEM and vice versa.</span></span> 

<span data-ttu-id="3997c-144">Para converter um arquivo PEM em PFX, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="3997c-144">To convert from a PEM file to a PFX file, use the following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="3997c-145">Para converter um arquivo PFX em PEM, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="3997c-145">To convert from a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="3997c-146">Consulte [documentação OpenSSL](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) para ver os detalhes.</span><span class="sxs-lookup"><span data-stu-id="3997c-146">Refer to [OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="3997c-147">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="3997c-147">Troubleshooting</span></span>


### <a name="copying-of-the-application-package-does-not-succeed"></a><span data-ttu-id="3997c-148">A cópia do pacote de aplicativos não é bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="3997c-148">Copying of the application package does not succeed</span></span>

<span data-ttu-id="3997c-149">Verifique se `openssh` está instalado.</span><span class="sxs-lookup"><span data-stu-id="3997c-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="3997c-150">Por padrão, a área de trabalho do Ubuntu não está instalada.</span><span class="sxs-lookup"><span data-stu-id="3997c-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="3997c-151">Instale-o usando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3997c-151">Install it using the following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="3997c-152">Se o problema persistir, tente desabilitar o PAM para ssh alterando o arquivo `sshd_config` usando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="3997c-152">If the problem persists, try disabling PAM for ssh by changing the `sshd_config` file using the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change the line with UsePAM to the following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="3997c-153">Se o problema persistir, tente aumentar o número de sessões ssh executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="3997c-153">If the problem still persists, try increasing the number of ssh sessions by executing the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add the following to lines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="3997c-154">O uso de chaves para autenticação ssh (em vez de senhas) ainda não tem suporte (porque a plataforma usa ssh para copiar os pacotes), portanto use a autenticação de senha.</span><span class="sxs-lookup"><span data-stu-id="3997c-154">Using keys for ssh authentication (as opposed to passwords) isn't yet supported (since the platform uses ssh to copy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3997c-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3997c-155">Next steps</span></span>

[<span data-ttu-id="3997c-156">Configurar o ambiente de desenvolvimento e implantar um aplicativo do Service Fabric em um cluster do Linux.</span><span class="sxs-lookup"><span data-stu-id="3997c-156">Set up the development environment and deploy a Service Fabric application to a Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="3997c-157">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="3997c-157">Related articles</span></span>

* [<span data-ttu-id="3997c-158">Introdução ao Service Fabric e à CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="3997c-158">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
