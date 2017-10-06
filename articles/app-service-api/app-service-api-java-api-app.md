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
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a>Criar e implantar um aplicativo de API Java no Serviço de Aplicativo do Azure
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Este tutorial mostra como toocreate um aplicativo Java e implantá-lo em aplicativos de API do serviço de aplicativo tooAzure usando [Git]. instruções de saudação neste tutorial podem ser seguidas em qualquer sistema operacional que é capaz de executar Java. código de saudação neste tutorial é criado usando [Maven]. [RS JAX] é usado toocreate hello serviço RESTful e é gerado com base em Olá [Swagger] especificação de metadados usando Olá [Swagger Editor].

## <a name="prerequisites"></a>Pré-requisitos
1. [Java Developer's Kit 8] \(ou posterior)
2. [Maven] instalado na máquina de desenvolvimento
3. [Git] instalado na máquina de desenvolvimento
4. Um pagos ou [avaliação gratuita] assinatura muito[Microsoft Azure]
5. Um aplicativo de teste HTTP como [carteiro]

## <a name="scaffold-hello-api-using-swaggerio"></a>API de saudação Scaffold usando Swagger.IO
Usando o editor do hello swagger.io online, você pode inserir o código de Swagger JSON ou YAML que representa a estrutura de saudação da sua API. Uma vez que a área de superfície de API do hello criada, você pode exportar o código para uma variedade de plataformas e estruturas. Na próxima seção, Olá, o código de saudação Scaffold será modificado tooinclude funcionalidade de simulação. 

Esta demonstração começa com um corpo JSON Swagger que será colada no editor de swagger.io hello, que será, em seguida, ser usado toogenerate código fazendo uso do RS JAX tooaccess um ponto de extremidade da API REST. Em seguida, você editará dados fictícios de saudação Scaffold código tooreturn, simulando uma API REST construído sobre um mecanismo de persistência de dados.  

1. Copie Olá área de transferência do JSON Swagger código tooyour a seguir:
   
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
2. Navegue toohello [Editor Online Swagger]. Uma vez, clique em Olá **arquivo -> Colar JSON** item de menu.
   
    ![Colar item de menu JSON][paste-json]
3. Cole Olá contatos lista API Swagger JSON copiados anteriormente. 
   
    ![Colar código JSON no Swagger][pasted-swagger]
4. Exibir páginas de documentação do hello e renderizado no editor de saudação de resumo de API. 
   
    ![Exibir Documentos Gerados pelo Swagger][view-swagger-generated-docs]
5. Selecione Olá **gerar Server -> JAX RS** código menu opção tooscaffold saudação do servidor você editará a implementação de simulação tooadd posterior. 
   
    ![Gerar Item de Menu de Código][generate-code-menu-item]
   
    Depois que o código de saudação é gerado, você terá um toodownload do arquivo ZIP. Esse arquivo contém código Olá Scaffold pelo gerador de código de Swagger de saudação e todos os associados criar scripts. Descompacte o diretório de tooa Olá toda a biblioteca em sua estação de trabalho de desenvolvimento. 

## <a name="edit-hello-code-tooadd-api-implementation"></a>Editar saudação código tooadd implementação da API
Nesta seção, você substituirá Olá gerado Swagger do lado do servidor implementação de código com o código personalizado. novo código de saudação retornará um cliente de chamada de toohello de entidades ArrayList de contato. 

1. Olá abrir *Contact.java* arquivo de modelo, que está localizado em Olá *src/gen / / e/s/swagger/modelo java* pasta, usando [código do Visual Studio] ou seu editor de texto favorito. 
   
    ![Abrir Arquivo de Modelo de Contato][open-contact-model-file]
2. Adicionar Olá construtor dentro Olá a seguir **contato** classe. 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. Olá abrir *ContactsApiServiceImpl.java* arquivo de implementação de serviço, que está localizado em Olá *src/main/java/e/s/swagger/api/implementação* pasta, usando [código do Visual Studio]ou seu editor de texto favorito.
   
    ![Abrir Arquivo de Código de Serviço de Contato][open-contact-service-code-file]
4. Substitua o código de Olá no arquivo hello com esse novo tooadd de código um código de serviço toohello implementação fictícia. 
   
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
5. Abra um prompt de comando e altere a pasta do diretório toohello raiz do seu aplicativo.
6. Execute Olá após Maven comando toobuild Olá código e executá-lo usando Olá servidor de aplicativos do Jetty localmente. 
   
        mvn package jetty:run
7. Você deve ver a janela de comando Olá refletir Jetty iniciou o código na porta 8080. 
   
    ![Abrir Arquivo de Código de Serviço de Contato][run-jetty-war]
8. Use [carteiro] método toomake uma solicitação toohello "obter todos os contatos" API na api/http://localhost:8080/contatos.
   
    ![Saudação de chamada da API de contatos][calling-contacts-api]
9. Use [carteiro] método toomake uma solicitação toohello "obter contato específico" API localizado em http://localhost:8080/api/contatos/2.
   
    ![Saudação de chamada da API de contatos][calling-specific-contact-api]
10. Por fim, compile o arquivo de Java WAR (arquivo Web) do hello executando Olá Maven comando no seu console a seguir. 
    
         mvn package war:war
11. Depois que o arquivo WAR de saudação é criado, ele será colocado em Olá **destino** pasta. Navegue até Olá **destino** pasta e renomeie Olá arquivo WAR muito**ROOT.war**. (Verifique se capitalização Olá corresponda a este formato).
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. Por fim, execute Olá comandos a seguir na pasta raiz de saudação do seu aplicativo toocreate um **implantar** Olá toodeploy de toouse pasta WAR tooAzure do arquivo. 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a>Publicar Olá tooAzure de saída do serviço de aplicativo
Nesta seção, você aprenderá como toocreate um App API novo usando Olá Portal do Azure, preparar essa API App para hospedar aplicativos Java e implantar Olá recém-criado WAR arquivo tooAzure toorun do serviço de aplicativo a new App API. 

1. Criar um novo aplicativo de API no hello [portal do Azure], clicando em Olá **Novo -> Web + móvel -> aplicativo de API** item de menu, digitando os detalhes do aplicativo e, em seguida, clicando em **criar**.
   
    ![Criar um novo Aplicativo de API][create-api-app]
2. Depois que seu aplicativo de API foi criado, abra o aplicativo **configurações** folha e, em seguida, clique em Olá **configurações de aplicativo** item de menu. Selecione Olá versões mais recentes do Java de opções disponíveis de hello, em seguida, selecione Olá Tomcat mais recente da saudação **contêiner da Web** menu e clique **salvar**.
   
    ![Configurar Java no hello folha API App][set-up-java]
3. Clique em Olá **credenciais de implantação** menu Configurações do item e forneça um nome de usuário e senha que você deseja toouse para publicar arquivos tooyour API App. 
   
    ![Definir credenciais de implantação][deployment-credentials]
4. Clique em Olá **origem de implantação** item de menu de configurações. Uma vez, clique em Olá **Escolher fonte** botão, selecione Olá **repositório Git Local** opção e, em seguida, clique em **Okey**. Isso criará um repositório Git em execução no Azure, com uma associação ao seu Aplicativo de API. Cada vez que você confirmar que o código toohello *mestre* ramificação do repositório Git, seu código será publicado em sua instância de API App em execução ao vivo. 
   
    ![Configurar um novo repositório Git local][select-git-repo]
5. URL tooyour na área de transferência do cópia Olá novo repositório Git. Salve-a porque ela será importante daqui a pouco. 
   
    ![Configurar um novo repositório Git para o aplicativo][copy-git-repo-url]
6. Git por push Olá WAR arquivo toohello repositório on-line. toodo isso, navegue até Olá **implantar** pasta que você criou anteriormente para que você pode facilmente confirmar código Olá backup toohello repositório em execução no seu serviço de aplicativo. Uma vez você estiver na janela de console hello e navegar na pasta Olá onde está localizada, a pasta webapps de saudação emitir Olá seguindo o processo de saudação do Git comandos toolaunch e disparar uma implantação. 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    Depois de você emitir Olá **push** solicitação, você será solicitado para senha Olá criado anteriormente para credenciais de implantação de saudação. Depois de inserir suas credenciais, você deverá ver a exibição do portal que Olá atualização foi implantada.
7. Se você usar novamente carteiro toohit Olá recentemente implantados App API em execução no serviço de aplicativo do Azure, você verá que o comportamento de saudação é consistente e que agora ele está retornando dados de contato conforme o esperado, e usar as alterações de código simples toohello Swagger.io Scaffold código Java. 
   
    ![Usando a API REST de Contatos Java dinamicamente no Azure][postman-calling-azure-contacts]

## <a name="next-steps"></a>Próximas etapas
Neste artigo, era possível toostart com um arquivo Swagger JSON e algum código Java scaffolding obtido do editor de Swagger.io hello. A partir daí, suas alterações simples e um processo de implantação Git resultaram em um aplicativo de API funcional escrito em Java. tutorial de Avançar Olá mostra como muito[consumir aplicativos de API de clientes JavaScript usando CORS][App Service API CORS]. Tutoriais posteriores Olá série mostrar como tooimplement autenticação e autorização.

toobuild nesse exemplo, você pode aprender mais sobre Olá [Storage SDK para Java] blobs do toopersist Olá JSON. Ou, você pode usar o hello [SDK de Java do banco de dados de documento] toosave seu dados de contato tooAzure banco de dados de documento. 

<a name="see-also"></a>

## <a name="see-also"></a>Consulte também
Para saber mais sobre como usar o Azure com o Java, visite [Azure para desenvolvedores Java](/java/azure).

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
