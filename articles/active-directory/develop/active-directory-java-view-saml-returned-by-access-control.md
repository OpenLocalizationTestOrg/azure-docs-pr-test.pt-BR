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
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a><span data-ttu-id="cfa97-103">Como tooview SAML retornado pelo hello Azure Access Control Service</span><span class="sxs-lookup"><span data-stu-id="cfa97-103">How tooview SAML returned by hello Azure Access Control Service</span></span>
<span data-ttu-id="cfa97-104">Este guia mostrará como Olá tooview subjacente SAML Security Assertion Markup Language () retornado tooyour aplicativo por hello Azure Access Control Service (ACS).</span><span class="sxs-lookup"><span data-stu-id="cfa97-104">This guide will show you how tooview hello underlying Security Assertion Markup Language (SAML) returned tooyour application by hello Azure Access Control Service (ACS).</span></span> <span data-ttu-id="cfa97-105">guia Olá baseia Olá [como tooAuthenticate usuários da Web com o Azure acesso de controle de serviço usando o Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) tópico, fornecendo o código que exibe informações de SAML hello.</span><span class="sxs-lookup"><span data-stu-id="cfa97-105">hello guide builds on hello [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays hello SAML information.</span></span> <span data-ttu-id="cfa97-106">aplicativo Hello concluída será a aparência a seguir toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="cfa97-106">hello completed application will look similar toohello following.</span></span>

![Saída do SAML de exemplo][saml_output]

<span data-ttu-id="cfa97-108">Para obter mais informações sobre o ACS, consulte Olá [próximas etapas](#next_steps) seção.</span><span class="sxs-lookup"><span data-stu-id="cfa97-108">For more information on ACS, see hello [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="cfa97-109">Olá filtro de controle de serviços de acesso do Azure é uma visualização de tecnologia da comunidade.</span><span class="sxs-lookup"><span data-stu-id="cfa97-109">hello Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="cfa97-110">Como software de pré-lançamento, a Microsoft não dá suporte formal a ele.</span><span class="sxs-lookup"><span data-stu-id="cfa97-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="cfa97-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cfa97-111">Prerequisites</span></span>
<span data-ttu-id="cfa97-112">tarefas de saudação toocomplete neste guia, completa Olá amostra em [como tooAuthenticate usuários da Web com o Azure acesso de controle de serviço usando o Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) e usá-lo como ponto de partida para este tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="cfa97-112">toocomplete hello tasks in this guide, complete hello sample at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as hello starting point for this tutorial.</span></span>

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a><span data-ttu-id="cfa97-113">Adicionar Olá JspWriter tooyour compilação implantação e o caminho do assembly de biblioteca</span><span class="sxs-lookup"><span data-stu-id="cfa97-113">Add hello JspWriter library tooyour build path and deployment assembly</span></span>
<span data-ttu-id="cfa97-114">Adicionar a biblioteca de saudação que contém Olá **javax.servlet.jsp.JspWriter** tooyour classe compilar o assembly de implantação e de caminho.</span><span class="sxs-lookup"><span data-stu-id="cfa97-114">Add hello library that contains hello **javax.servlet.jsp.JspWriter** class tooyour build path and deployment assembly.</span></span> <span data-ttu-id="cfa97-115">Se você estiver usando o Tomcat, biblioteca de saudação é **jsp-API. jar**, que está localizado na Olá Apache **lib** pasta.</span><span class="sxs-lookup"><span data-stu-id="cfa97-115">If you are using Tomcat, hello library is **jsp-api.jar**, which is located in hello Apache **lib** folder.</span></span>

1. <span data-ttu-id="cfa97-116">No Explorador de projeto do Eclipse, clique com botão direito **MyACSHelloWorld**, clique em **caminho de compilação de**, clique em **caminho de compilação de configurar**, clique em Olá **bibliotecas** guia e, em seguida, clique em **adicionar JARs externo**.</span><span class="sxs-lookup"><span data-stu-id="cfa97-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click hello **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="cfa97-117">Em Olá **seleção JAR** caixa de diálogo, navegue toohello JAR necessário, selecione-o e, em seguida, clique em **abrir**.</span><span class="sxs-lookup"><span data-stu-id="cfa97-117">In hello **JAR Selection** dialog, navigate toohello necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="cfa97-118">Com hello **propriedades MyACSHelloWorld** caixa de diálogo aberta, clique **Assembly de implantação**.</span><span class="sxs-lookup"><span data-stu-id="cfa97-118">With hello **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="cfa97-119">Em Olá **Assembly de implantação da Web** caixa de diálogo, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cfa97-119">In hello **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="cfa97-120">Em Olá **nova diretiva de Assembly** caixa de diálogo, clique em **entradas de caminho de compilação Java** e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="cfa97-120">In hello **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="cfa97-121">Selecione a biblioteca apropriada hello e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="cfa97-121">Select hello appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="cfa97-122">Clique em **Okey** tooclose Olá **propriedades MyACSHelloWorld** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cfa97-122">Click **OK** tooclose hello **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-hello-jsp-file-toodisplay-saml"></a><span data-ttu-id="cfa97-123">Modificar Olá JSP arquivo toodisplay SAML</span><span class="sxs-lookup"><span data-stu-id="cfa97-123">Modify hello JSP file toodisplay SAML</span></span>
<span data-ttu-id="cfa97-124">Modificar **index.jsp** toouse Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="cfa97-124">Modify **index.jsp** toouse hello following code.</span></span>

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

## <a name="run-hello-application"></a><span data-ttu-id="cfa97-125">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="cfa97-125">Run hello application</span></span>
1. <span data-ttu-id="cfa97-126">Executar o aplicativo no emulador de computação hello ou implantar tooAzure, usando as etapas Olá documentadas em [como tooAuthenticate usuários da Web com o Azure acesso de controle de serviço usando o Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="cfa97-126">Run your application in hello computer emulator or deploy tooAzure, using hello steps documented at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="cfa97-127">Inicie um navegador e abra o aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="cfa97-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="cfa97-128">Depois de fazer logon tooyour aplicativo, você verá informações de SAML, incluindo a asserção de segurança Olá fornecida pelo provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="cfa97-128">After you log on tooyour application, you'll see SAML information, including hello security assertion provided by hello identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfa97-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cfa97-129">Next steps</span></span>
<span data-ttu-id="cfa97-130">toofurther explorar tooexperiment com cenários mais sofisticados e funcionalidade do ACS, consulte [Access Control Service 2.0][Access Control Service 2.0].</span><span class="sxs-lookup"><span data-stu-id="cfa97-130">toofurther explore ACS's functionality and tooexperiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
