---
title: "aaaView SAML retornado pelo Olá Access Control Service (Java)"
description: "Saiba como tooview SAML retornado pelo Olá serviço de controle de acesso em aplicativos Java hospedados no Azure."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6cd216f9-eb43-46b4-b30d-f194d0ae2d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: b6733bc98b505cfa89a4ce456f368ee15da11427
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a>Como tooview SAML retornado pelo hello Azure Access Control Service
Este guia mostrará como Olá tooview subjacente SAML Security Assertion Markup Language () retornado tooyour aplicativo por hello Azure Access Control Service (ACS). guia Olá baseia Olá [como tooAuthenticate usuários da Web com o Azure acesso de controle de serviço usando o Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) tópico, fornecendo o código que exibe informações de SAML hello. aplicativo Hello concluída será a aparência a seguir toohello semelhante.

![Saída do SAML de exemplo][saml_output]

Para obter mais informações sobre o ACS, consulte Olá [próximas etapas](#next_steps) seção.

> [!NOTE]
> Olá filtro de controle de serviços de acesso do Azure é uma visualização de tecnologia da comunidade. Como software de pré-lançamento, a Microsoft não dá suporte formal a ele.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
tarefas de saudação toocomplete neste guia, completa Olá amostra em [como tooAuthenticate usuários da Web com o Azure acesso de controle de serviço usando o Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) e usá-lo como ponto de partida para este tutorial de saudação.

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a>Adicionar Olá JspWriter tooyour compilação implantação e o caminho do assembly de biblioteca
Adicionar a biblioteca de saudação que contém Olá **javax.servlet.jsp.JspWriter** tooyour classe compilar o assembly de implantação e de caminho. Se você estiver usando o Tomcat, biblioteca de saudação é **jsp-API. jar**, que está localizado na Olá Apache **lib** pasta.

1. No Explorador de projeto do Eclipse, clique com botão direito **MyACSHelloWorld**, clique em **caminho de compilação de**, clique em **caminho de compilação de configurar**, clique em Olá **bibliotecas** guia e, em seguida, clique em **adicionar JARs externo**.
2. Em Olá **seleção JAR** caixa de diálogo, navegue toohello JAR necessário, selecione-o e, em seguida, clique em **abrir**.
3. Com hello **propriedades MyACSHelloWorld** caixa de diálogo aberta, clique **Assembly de implantação**.
4. Em Olá **Assembly de implantação da Web** caixa de diálogo, clique em **adicionar**.
5. Em Olá **nova diretiva de Assembly** caixa de diálogo, clique em **entradas de caminho de compilação Java** e, em seguida, clique em **próximo**.
6. Selecione a biblioteca apropriada hello e clique em **concluir**.
7. Clique em **Okey** tooclose Olá **propriedades MyACSHelloWorld** caixa de diálogo.

## <a name="modify-hello-jsp-file-toodisplay-saml"></a>Modificar Olá JSP arquivo toodisplay SAML
Modificar **index.jsp** toouse Olá código a seguir.

    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
        <%@ page import="javax.xml.parsers.*"
                 import="javax.xml.transform.*"
                 import="org.w3c.dom.*"
                 import="java.io.*"
                 import="javax.xml.transform.stream.*"
                 import="javax.xml.transform.dom.*"
                 import="javax.xml.xpath.*"
                 import="javax.servlet.jsp.JspWriter" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Sample ACS Filter</title>
    </head>
    <body>
        <h3>SAML information from sample ACS program</h3>
        <%!
        void displaySAMLInfo(Node node, String parent, JspWriter out)
        {

            try
            {
                String nodeName;
                int nChild, i;

                nodeName = node.getNodeName();
                out.println("<br>");
                out.println("<u>Examining <b>" + parent + nodeName + "</b></u><br>");

                   // Attributes.
                   NamedNodeMap attribsMap = node.getAttributes();
                   if (null != attribsMap)
                   {
                         for (i=0; i < attribsMap.getLength(); i++)
                         {
                                Node attrib = attribsMap.item(i);
                                out.println("Attribute: <b>" + attrib.getNodeName() + "</b>: " + attrib.getNodeValue()  + "<br>");
                         }
                   }

                   // Child nodes.
                   NodeList list = node.getChildNodes();
                   if (null != list)
                    {
                          nChild = list.getLength();
                          if (nChild > 0)
                          {                    

                                 // If it is a text node, just print hello text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out hello child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate hello names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish hello sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process hello child nodes.
                                     for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);
                                        displaySAMLInfo(temp, parent + nodeName + "\\", out);
                                     }
                               }
                          }
                      }
                  }
                catch (Exception e)
                {
                    System.out.println("Exception encountered.");
                    e.printStackTrace();            
                }
            }
        %>

        <%
        try
        {
            String data  = (String) request.getAttribute("ACSSAML");

            DocumentBuilder docBuilder;
            Document doc = null;
            DocumentBuilderFactory docBuilderFactory = DocumentBuilderFactory.newInstance();
            docBuilderFactory.setIgnoringElementContentWhitespace(true);
            docBuilder = docBuilderFactory.newDocumentBuilder();
            byte[] xmlDATA = data.getBytes();

            ByteArrayInputStream in = new ByteArrayInputStream(xmlDATA);
            doc = docBuilder.parse(in);
            doc.getDocumentElement().normalize();

            // Iterate hello child nodes of hello doc.
            NodeList list = doc.getChildNodes();

            for (int i=0; i < list.getLength(); i++)
            {
                displaySAMLInfo(list.item(i), "", out);
            }
        }
        catch (Exception e)
        {
            out.println("Exception encountered.");
            e.printStackTrace();
        }

        %>
    </body>
    </html>

## <a name="run-hello-application"></a>Executar o aplicativo hello
1. Executar o aplicativo no emulador de computação hello ou implantar tooAzure, usando as etapas Olá documentadas em [como tooAuthenticate usuários da Web com o Azure acesso de controle de serviço usando o Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).
2. Inicie um navegador e abra o aplicativo web. Depois de fazer logon tooyour aplicativo, você verá informações de SAML, incluindo a asserção de segurança Olá fornecida pelo provedor de identidade hello.

## <a name="next-steps"></a>Próximas etapas
toofurther explorar tooexperiment com cenários mais sofisticados e funcionalidade do ACS, consulte [Access Control Service 2.0][Access Control Service 2.0].

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
