---
title: "aaaBuild e implantar um aplicativo de API do Java no serviço de aplicativo do Azure"
description: "Saiba como toocreate um aplicativo de API do Java de pacote e implantá-lo tooAzure do serviço de aplicativo."
services: app-service\api
documentationcenter: java
author: rmcmurray
manager: erikre
editor: tdykstra
ms.assetid: 8d21ba5f-fc57-4269-bc8f-2fcab936ec22
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: get-started-article
ms.date: 04/25/2017
ms.author: rachelap;robmcm
ms.openlocfilehash: a4056fec870b1c4bed8ee14bb0e748b3ee89b9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="964b4-103">Criar e implantar um aplicativo de API Java no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="964b4-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="964b4-104">Este tutorial mostra como toocreate um aplicativo Java e implantá-lo em aplicativos de API do serviço de aplicativo tooAzure usando [Git].</span><span class="sxs-lookup"><span data-stu-id="964b4-104">This tutorial shows how toocreate a Java application and deploy it tooAzure App Service API Apps using [Git].</span></span> <span data-ttu-id="964b4-105">instruções de saudação neste tutorial podem ser seguidas em qualquer sistema operacional que é capaz de executar Java.</span><span class="sxs-lookup"><span data-stu-id="964b4-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="964b4-106">código de saudação neste tutorial é criado usando [Maven].</span><span class="sxs-lookup"><span data-stu-id="964b4-106">hello code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="964b4-107">[RS JAX] é usado toocreate hello serviço RESTful e é gerado com base em Olá [Swagger] especificação de metadados usando Olá [Swagger Editor].</span><span class="sxs-lookup"><span data-stu-id="964b4-107">[Jax-RS] is used toocreate hello RESTful Service, and is generated based on hello [Swagger] metadata specification using hello [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="964b4-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="964b4-108">Prerequisites</span></span>
1. <span data-ttu-id="964b4-109">[Java Developer's Kit 8] \(ou posterior)</span><span class="sxs-lookup"><span data-stu-id="964b4-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="964b4-110">[Maven] instalado na máquina de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="964b4-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="964b4-111">[Git] instalado na máquina de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="964b4-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="964b4-112">Um pagos ou [avaliação gratuita] assinatura muito[Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="964b4-112">A paid or [free trial] subscription too[Microsoft Azure]</span></span>
5. <span data-ttu-id="964b4-113">Um aplicativo de teste HTTP como [carteiro]</span><span class="sxs-lookup"><span data-stu-id="964b4-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-hello-api-using-swaggerio"></a><span data-ttu-id="964b4-114">API de saudação Scaffold usando Swagger.IO</span><span class="sxs-lookup"><span data-stu-id="964b4-114">Scaffold hello API using Swagger.IO</span></span>
<span data-ttu-id="964b4-115">Usando o editor do hello swagger.io online, você pode inserir o código de Swagger JSON ou YAML que representa a estrutura de saudação da sua API.</span><span class="sxs-lookup"><span data-stu-id="964b4-115">Using hello swagger.io online editor, you can enter Swagger JSON or YAML code representing hello structure of your API.</span></span> <span data-ttu-id="964b4-116">Uma vez que a área de superfície de API do hello criada, você pode exportar o código para uma variedade de plataformas e estruturas.</span><span class="sxs-lookup"><span data-stu-id="964b4-116">Once you have hello API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="964b4-117">Na próxima seção, Olá, o código de saudação Scaffold será modificado tooinclude funcionalidade de simulação.</span><span class="sxs-lookup"><span data-stu-id="964b4-117">In hello next section, hello scaffolded code will be modified tooinclude mock functionality.</span></span> 

<span data-ttu-id="964b4-118">Esta demonstração começa com um corpo JSON Swagger que será colada no editor de swagger.io hello, que será, em seguida, ser usado toogenerate código fazendo uso do RS JAX tooaccess um ponto de extremidade da API REST.</span><span class="sxs-lookup"><span data-stu-id="964b4-118">This demonstration will begin with a Swagger JSON body that you will paste into hello swagger.io editor, which will then be used toogenerate code making use of JAX-RS tooaccess a REST API endpoint.</span></span> <span data-ttu-id="964b4-119">Em seguida, você editará dados fictícios de saudação Scaffold código tooreturn, simulando uma API REST construído sobre um mecanismo de persistência de dados.</span><span class="sxs-lookup"><span data-stu-id="964b4-119">Then, you'll edit hello scaffolded code tooreturn mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="964b4-120">Copie Olá área de transferência do JSON Swagger código tooyour a seguir:</span><span class="sxs-lookup"><span data-stu-id="964b4-120">Copy hello following Swagger JSON code tooyour clipboard:</span></span>
   
        {
            "swagger": "2.0",
            "info": {
                "version": "v1",
                "title": "Contact List",
                "description": "A Contact list API based on Swagger and built using Java"
            },
            "host": "localhost",
            "schemes": [
                "http",
                "https"
            ],
            "basePath": "/api",
            "paths": {
                "/contacts": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_get",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                },
                "/contacts/{id}": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_getById",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "parameters": [
                            {
                                "name": "id",
                                "in": "path",
                                "required": true,
                                "type": "integer",
                                "format": "int32"
                            }
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                }
            },
            "definitions": {
                "Contact": {
                    "type": "object",
                    "properties": {
                        "Id": {
                            "format": "int32",
                            "type": "integer"
                        },
                        "Name": {
                            "type": "string"
                        },
                        "EmailAddress": {
                            "type": "string"
                        }
                    }
                }
            }
        }
2. <span data-ttu-id="964b4-121">Navegue toohello [Editor Online Swagger].</span><span class="sxs-lookup"><span data-stu-id="964b4-121">Navigate toohello [Online Swagger Editor].</span></span> <span data-ttu-id="964b4-122">Uma vez, clique em Olá **arquivo -> Colar JSON** item de menu.</span><span class="sxs-lookup"><span data-stu-id="964b4-122">Once there, click hello **File -> Paste JSON** menu item.</span></span>
   
    ![Colar item de menu JSON][paste-json]
3. <span data-ttu-id="964b4-124">Cole Olá contatos lista API Swagger JSON copiados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="964b4-124">Paste in hello Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![Colar código JSON no Swagger][pasted-swagger]
4. <span data-ttu-id="964b4-126">Exibir páginas de documentação do hello e renderizado no editor de saudação de resumo de API.</span><span class="sxs-lookup"><span data-stu-id="964b4-126">View hello documentation pages and API summary rendered in hello editor.</span></span> 
   
    ![Exibir Documentos Gerados pelo Swagger][view-swagger-generated-docs]
5. <span data-ttu-id="964b4-128">Selecione Olá **gerar Server -> JAX RS** código menu opção tooscaffold saudação do servidor você editará a implementação de simulação tooadd posterior.</span><span class="sxs-lookup"><span data-stu-id="964b4-128">Select hello **Generate Server -> JAX-RS** menu option tooscaffold hello server-side code you'll edit later tooadd mock implementation.</span></span> 
   
    ![Gerar Item de Menu de Código][generate-code-menu-item]
   
    <span data-ttu-id="964b4-130">Depois que o código de saudação é gerado, você terá um toodownload do arquivo ZIP.</span><span class="sxs-lookup"><span data-stu-id="964b4-130">Once hello code is generated, you'll be provided a ZIP file toodownload.</span></span> <span data-ttu-id="964b4-131">Esse arquivo contém código Olá Scaffold pelo gerador de código de Swagger de saudação e todos os associados criar scripts.</span><span class="sxs-lookup"><span data-stu-id="964b4-131">This file contains hello code scaffolded by hello Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="964b4-132">Descompacte o diretório de tooa Olá toda a biblioteca em sua estação de trabalho de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="964b4-132">Unzip hello entire library tooa directory on your development workstation.</span></span> 

## <a name="edit-hello-code-tooadd-api-implementation"></a><span data-ttu-id="964b4-133">Editar saudação código tooadd implementação da API</span><span class="sxs-lookup"><span data-stu-id="964b4-133">Edit hello Code tooadd API Implementation</span></span>
<span data-ttu-id="964b4-134">Nesta seção, você substituirá Olá gerado Swagger do lado do servidor implementação de código com o código personalizado.</span><span class="sxs-lookup"><span data-stu-id="964b4-134">In this section, you'll replace hello Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="964b4-135">novo código de saudação retornará um cliente de chamada de toohello de entidades ArrayList de contato.</span><span class="sxs-lookup"><span data-stu-id="964b4-135">hello new code will return an ArrayList of Contact entities toohello calling client.</span></span> 

1. <span data-ttu-id="964b4-136">Olá abrir *Contact.java* arquivo de modelo, que está localizado em Olá *src/gen / / e/s/swagger/modelo java* pasta, usando [código do Visual Studio] ou seu editor de texto favorito.</span><span class="sxs-lookup"><span data-stu-id="964b4-136">Open hello *Contact.java* model file, which is located in hello *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![Abrir Arquivo de Modelo de Contato][open-contact-model-file]
2. <span data-ttu-id="964b4-138">Adicionar Olá construtor dentro Olá a seguir **contato** classe.</span><span class="sxs-lookup"><span data-stu-id="964b4-138">Add hello following constructor within hello **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="964b4-139">Olá abrir *ContactsApiServiceImpl.java* arquivo de implementação de serviço, que está localizado em Olá *src/main/java/e/s/swagger/api/implementação* pasta, usando [código do Visual Studio]ou seu editor de texto favorito.</span><span class="sxs-lookup"><span data-stu-id="964b4-139">Open hello *ContactsApiServiceImpl.java* service implementation file, which is located in hello *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![Abrir Arquivo de Código de Serviço de Contato][open-contact-service-code-file]
4. <span data-ttu-id="964b4-141">Substitua o código de Olá no arquivo hello com esse novo tooadd de código um código de serviço toohello implementação fictícia.</span><span class="sxs-lookup"><span data-stu-id="964b4-141">Overwrite hello code in hello file with this new code tooadd a mock implementation toohello service code.</span></span> 
   
        package io.swagger.api.impl;
   
        import io.swagger.api.*;
        
        import io.swagger.model.Contact;
        import java.util.*;
        import io.swagger.api.NotFoundException;
               
        import javax.ws.rs.core.Response;
        import javax.ws.rs.core.SecurityContext;
   
        @javax.annotation.Generated(value = "class io.swagger.codegen.languages.JaxRSServerCodegen", date = "2015-11-24T21:54:11.648Z")
        public class ContactsApiServiceImpl extends ContactsApiService {
   
            private ArrayList<Contact> loadContacts()
            {
                ArrayList<Contact> list = new ArrayList<Contact>();
                list.add(new Contact(1, "Barney Poland", "barney@contoso.com"));
                list.add(new Contact(2, "Lacy Barrera", "lacy@contoso.com"));
                list.add(new Contact(3, "Lora Riggs", "lora@contoso.com"));
                return list;
            }
   
            @Override
            public Response contactsGet(SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                return Response.ok().entity(list).build();
                }
   
            @Override
            public Response contactsGetById(Integer id, SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                Contact ret = null;
   
                for(int i=0; i<list.size(); i++)
                {
                    if(list.get(i).getId() == id)
                        {
                            ret = list.get(i);
                        }
                }
                return Response.ok().entity(ret).build();
            }
        }
5. <span data-ttu-id="964b4-142">Abra um prompt de comando e altere a pasta do diretório toohello raiz do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="964b4-142">Open a command prompt and change directory toohello root folder of your application.</span></span>
6. <span data-ttu-id="964b4-143">Execute Olá após Maven comando toobuild Olá código e executá-lo usando Olá servidor de aplicativos do Jetty localmente.</span><span class="sxs-lookup"><span data-stu-id="964b4-143">Execute hello following Maven command toobuild hello code and run it using hello Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="964b4-144">Você deve ver a janela de comando Olá refletir Jetty iniciou o código na porta 8080.</span><span class="sxs-lookup"><span data-stu-id="964b4-144">You should see hello command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![Abrir Arquivo de Código de Serviço de Contato][run-jetty-war]
8. <span data-ttu-id="964b4-146">Use [carteiro] método toomake uma solicitação toohello "obter todos os contatos" API na api/http://localhost:8080/contatos.</span><span class="sxs-lookup"><span data-stu-id="964b4-146">Use [Postman] toomake a request toohello "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![Saudação de chamada da API de contatos][calling-contacts-api]
9. <span data-ttu-id="964b4-148">Use [carteiro] método toomake uma solicitação toohello "obter contato específico" API localizado em http://localhost:8080/api/contatos/2.</span><span class="sxs-lookup"><span data-stu-id="964b4-148">Use [Postman] toomake a request toohello "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![Saudação de chamada da API de contatos][calling-specific-contact-api]
10. <span data-ttu-id="964b4-150">Por fim, compile o arquivo de Java WAR (arquivo Web) do hello executando Olá Maven comando no seu console a seguir.</span><span class="sxs-lookup"><span data-stu-id="964b4-150">Finally, build hello Java WAR (Web ARchive) file by executing hello following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="964b4-151">Depois que o arquivo WAR de saudação é criado, ele será colocado em Olá **destino** pasta.</span><span class="sxs-lookup"><span data-stu-id="964b4-151">Once hello WAR file is built, it will be placed into hello **target** folder.</span></span> <span data-ttu-id="964b4-152">Navegue até Olá **destino** pasta e renomeie Olá arquivo WAR muito**ROOT.war**.</span><span class="sxs-lookup"><span data-stu-id="964b4-152">Navigate into hello **target** folder and rename hello WAR file too**ROOT.war**.</span></span> <span data-ttu-id="964b4-153">(Verifique se capitalização Olá corresponda a este formato).</span><span class="sxs-lookup"><span data-stu-id="964b4-153">(Make sure hello capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="964b4-154">Por fim, execute Olá comandos a seguir na pasta raiz de saudação do seu aplicativo toocreate um **implantar** Olá toodeploy de toouse pasta WAR tooAzure do arquivo.</span><span class="sxs-lookup"><span data-stu-id="964b4-154">Finally, execute hello following commands from hello root folder of your application toocreate a **deploy** folder toouse toodeploy hello WAR file tooAzure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a><span data-ttu-id="964b4-155">Publicar Olá tooAzure de saída do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="964b4-155">Publish hello output tooAzure App Service</span></span>
<span data-ttu-id="964b4-156">Nesta seção, você aprenderá como toocreate um App API novo usando Olá Portal do Azure, preparar essa API App para hospedar aplicativos Java e implantar Olá recém-criado WAR arquivo tooAzure toorun do serviço de aplicativo a new App API.</span><span class="sxs-lookup"><span data-stu-id="964b4-156">In this section you'll learn how toocreate a new API App using hello Azure Portal, prepare that API App for hosting Java applications, and deploy hello newly-created WAR file tooAzure App Service toorun your new API App.</span></span> 

1. <span data-ttu-id="964b4-157">Criar um novo aplicativo de API no hello [portal do Azure], clicando em Olá **Novo -> Web + móvel -> aplicativo de API** item de menu, digitando os detalhes do aplicativo e, em seguida, clicando em **criar**.</span><span class="sxs-lookup"><span data-stu-id="964b4-157">Create a new API app in hello [Azure portal], by clicking hello **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![Criar um novo Aplicativo de API][create-api-app]
2. <span data-ttu-id="964b4-159">Depois que seu aplicativo de API foi criado, abra o aplicativo **configurações** folha e, em seguida, clique em Olá **configurações de aplicativo** item de menu.</span><span class="sxs-lookup"><span data-stu-id="964b4-159">Once your API app has been created, open your app's **Settings** blade, and then click hello **Application settings** menu item.</span></span> <span data-ttu-id="964b4-160">Selecione Olá versões mais recentes do Java de opções disponíveis de hello, em seguida, selecione Olá Tomcat mais recente da saudação **contêiner da Web** menu e clique **salvar**.</span><span class="sxs-lookup"><span data-stu-id="964b4-160">Select hello latest Java versions from hello available options, then select hello latest Tomcat from hello **Web container** menu, and then click **Save**.</span></span>
   
    ![Configurar Java no hello folha API App][set-up-java]
3. <span data-ttu-id="964b4-162">Clique em Olá **credenciais de implantação** menu Configurações do item e forneça um nome de usuário e senha que você deseja toouse para publicar arquivos tooyour API App.</span><span class="sxs-lookup"><span data-stu-id="964b4-162">Click hello **Deployment credentials** settings menu item, and provide a username and password you wish toouse for publishing files tooyour API App.</span></span> 
   
    ![Definir credenciais de implantação][deployment-credentials]
4. <span data-ttu-id="964b4-164">Clique em Olá **origem de implantação** item de menu de configurações.</span><span class="sxs-lookup"><span data-stu-id="964b4-164">Click hello **Deployment source** settings menu item.</span></span> <span data-ttu-id="964b4-165">Uma vez, clique em Olá **Escolher fonte** botão, selecione Olá **repositório Git Local** opção e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="964b4-165">Once there, click hello **Choose source** button, select hello **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="964b4-166">Isso criará um repositório Git em execução no Azure, com uma associação ao seu Aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="964b4-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="964b4-167">Cada vez que você confirmar que o código toohello *mestre* ramificação do repositório Git, seu código será publicado em sua instância de API App em execução ao vivo.</span><span class="sxs-lookup"><span data-stu-id="964b4-167">Each time you commit code toohello *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![Configurar um novo repositório Git local][select-git-repo]
5. <span data-ttu-id="964b4-169">URL tooyour na área de transferência do cópia Olá novo repositório Git.</span><span class="sxs-lookup"><span data-stu-id="964b4-169">Copy hello new Git repository's URL tooyour clipboard.</span></span> <span data-ttu-id="964b4-170">Salve-a porque ela será importante daqui a pouco.</span><span class="sxs-lookup"><span data-stu-id="964b4-170">Save this as it will be important in a moment.</span></span> 
   
    ![Configurar um novo repositório Git para o aplicativo][copy-git-repo-url]
6. <span data-ttu-id="964b4-172">Git por push Olá WAR arquivo toohello repositório on-line.</span><span class="sxs-lookup"><span data-stu-id="964b4-172">Git push hello WAR file toohello online repository.</span></span> <span data-ttu-id="964b4-173">toodo isso, navegue até Olá **implantar** pasta que você criou anteriormente para que você pode facilmente confirmar código Olá backup toohello repositório em execução no seu serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="964b4-173">toodo this, navigate into hello **deploy** folder you created earlier so that you can easily commit hello code up toohello repository running in your App Service.</span></span> <span data-ttu-id="964b4-174">Uma vez você estiver na janela de console hello e navegar na pasta Olá onde está localizada, a pasta webapps de saudação emitir Olá seguindo o processo de saudação do Git comandos toolaunch e disparar uma implantação.</span><span class="sxs-lookup"><span data-stu-id="964b4-174">Once you're in hello console window and navigated into hello folder where hello webapps folder is located, issue hello following Git commands toolaunch hello process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="964b4-175">Depois de você emitir Olá **push** solicitação, você será solicitado para senha Olá criado anteriormente para credenciais de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="964b4-175">Once you issue hello **push** request, you'll be asked for hello password you created for hello deployment credential earlier.</span></span> <span data-ttu-id="964b4-176">Depois de inserir suas credenciais, você deverá ver a exibição do portal que Olá atualização foi implantada.</span><span class="sxs-lookup"><span data-stu-id="964b4-176">After you enter your credentials, you should see your portal display that hello update was deployed.</span></span>
7. <span data-ttu-id="964b4-177">Se você usar novamente carteiro toohit Olá recentemente implantados App API em execução no serviço de aplicativo do Azure, você verá que o comportamento de saudação é consistente e que agora ele está retornando dados de contato conforme o esperado, e usar as alterações de código simples toohello Swagger.io Scaffold código Java.</span><span class="sxs-lookup"><span data-stu-id="964b4-177">If you once again use Postman toohit hello newly-deployed API App running in Azure App Service, you'll see that hello behavior is consistent and that now it is returning contact data as expected, and using simple code changes toohello Swagger.io scaffolded Java code.</span></span> 
   
    ![Usando a API REST de Contatos Java dinamicamente no Azure][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="964b4-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="964b4-179">Next steps</span></span>
<span data-ttu-id="964b4-180">Neste artigo, era possível toostart com um arquivo Swagger JSON e algum código Java scaffolding obtido do editor de Swagger.io hello.</span><span class="sxs-lookup"><span data-stu-id="964b4-180">In this article, you were able toostart with a Swagger JSON file and some scaffolded Java code obtained from hello Swagger.io editor.</span></span> <span data-ttu-id="964b4-181">A partir daí, suas alterações simples e um processo de implantação Git resultaram em um aplicativo de API funcional escrito em Java.</span><span class="sxs-lookup"><span data-stu-id="964b4-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="964b4-182">tutorial de Avançar Olá mostra como muito[consumir aplicativos de API de clientes JavaScript usando CORS][App Service API CORS].</span><span class="sxs-lookup"><span data-stu-id="964b4-182">hello next tutorial shows how too[consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="964b4-183">Tutoriais posteriores Olá série mostrar como tooimplement autenticação e autorização.</span><span class="sxs-lookup"><span data-stu-id="964b4-183">Later tutorials in hello series show how tooimplement authentication and authorization.</span></span>

<span data-ttu-id="964b4-184">toobuild nesse exemplo, você pode aprender mais sobre Olá [Storage SDK para Java] blobs do toopersist Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="964b4-184">toobuild on this sample, you can learn more about hello [Storage SDK for Java] toopersist hello JSON blobs.</span></span> <span data-ttu-id="964b4-185">Ou, você pode usar o hello [SDK de Java do banco de dados de documento] toosave seu dados de contato tooAzure banco de dados de documento.</span><span class="sxs-lookup"><span data-stu-id="964b4-185">Or, you could use hello [Document DB Java SDK] toosave your Contact data tooAzure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="964b4-186">Consulte também</span><span class="sxs-lookup"><span data-stu-id="964b4-186">See Also</span></span>
<span data-ttu-id="964b4-187">Para saber mais sobre como usar o Azure com o Java, visite [Azure para desenvolvedores Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="964b4-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[portal do Azure]: https://portal.azure.com/
[SDK de Java do banco de dados de documento]: ../documentdb/documentdb-java-application.md
[avaliação gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Java Developer's Kit 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[RS JAX]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[Editor Online Swagger]: http://editor2.swagger.io/
[carteiro]: https://www.getpostman.com/
[Storage SDK para Java]:../storage/blobs/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[Swagger Editor]: http://editor.swagger.io/
[código do Visual Studio]: https://code.visualstudio.com

<!-- IMG List -->

[paste-json]: ./media/app-service-api-java-api-app/paste-json.png
[pasted-swagger]: ./media/app-service-api-java-api-app/pasted-swagger.png
[view-swagger-generated-docs]: ./media/app-service-api-java-api-app/view-swagger-generated-docs.png
[generate-code-menu-item]: ./media/app-service-api-java-api-app/generate-code-menu-item.png
[open-contact-model-file]: ./media/app-service-api-java-api-app/open-contact-model-file.png
[open-contact-service-code-file]: ./media/app-service-api-java-api-app/open-contact-service-code-file.png
[run-jetty-war]: ./media/app-service-api-java-api-app/run-jetty-war.png
[calling-contacts-api]: ./media/app-service-api-java-api-app/calling-contacts-api.png
[calling-specific-contact-api]: ./media/app-service-api-java-api-app/calling-specific-contact-api.png
[create-api-app]: ./media/app-service-api-java-api-app/create-api-app.png
[set-up-java]: ./media/app-service-api-java-api-app/set-up-java.png
[deployment-credentials]: ./media/app-service-api-java-api-app/deployment-credentials.png
[select-git-repo]: ./media/app-service-api-java-api-app/select-git-repo.png
[copy-git-repo-url]: ./media/app-service-api-java-api-app/copy-git-repo-url.png
[postman-calling-azure-contacts]: ./media/app-service-api-java-api-app/postman-calling-azure-contacts.png
