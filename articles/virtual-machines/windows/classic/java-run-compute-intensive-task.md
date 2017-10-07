---
title: "aplicativo em uma máquina virtual Java que utiliza a aaaCompute | Microsoft Docs"
description: "Saiba como toocreate uma máquina virtual do Azure que executa um aplicativo de Java com computação intensiva que pode ser monitorado por outro aplicativo de Java."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a>Como toorun uma computação intensa de tarefas em Java em uma máquina virtual
> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

Com o Azure, você pode usar tarefas de computação intensa de toohandle uma máquina virtual. Por exemplo, uma máquina virtual pode lidar com tarefas e fornecer máquinas de tooclient resultados ou aplicativos móveis. Depois de ler este artigo, você terá uma compreensão de como toocreate uma máquina virtual que executa um aplicativo de Java com computação intensiva que pode ser monitorado por outro aplicativo de Java.

Este tutorial presume que você sabe como aplicativos de console de Java toocreate, pode importar um aplicativo de Java tooyour bibliotecas e pode gerar um JAR (Java archive). Nenhum conhecimento do Microsoft Azure é assumido.

Você aprenderá:

* Como toocreate uma máquina virtual com um Java Development Kit (JDK) já instalado.
* Como tooremotely fazem logon na máquina virtual de tooyour.
* Como toocreate um serviço de barramento de namespace.
* Como toocreate um aplicativo Java que executa uma tarefa de computação intensa.
* Como toocreate um aplicativo Java que monitora Olá progresso da tarefa de computação intensiva hello.
* Como toorun Olá aplicativos Java.
* Como toostop Olá aplicativos Java.

Este tutorial usará Olá problema do Caixeiro Viajante para tarefas de computação intensa hello. a seguir Olá é um exemplo de tarefa de computação intensa do hello Java aplicativo em execução hello.

![Solucionador de problemas do Caixeiro Viajante][solver_output]

a seguir Olá é um exemplo de hello Java aplicativo hello com computação intensiva a tarefa de monitoramento.

![Cliente de problemas do Caixeiro Viajante][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate uma máquina virtual
1. Faça logon no toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Clique em **Nova**, clique em **Computação**, clique em **Máquina virtual** e, em seguida, clique em **Da Galeria**.
3. Em Olá **select de imagem de máquina Virtual** caixa de diálogo, selecione **JDK 7 Windows Server 2012**.
   Observe que **JDK 6 Windows Server 2012** está disponível caso você tenha aplicativos herdados que ainda não estão pronto toorun JDK 7.
4. Clique em **Avançar**.
5. Em Olá **configuração de máquina Virtual** caixa de diálogo:
   1. Especifique um nome para a máquina virtual de saudação.
   2. Especifique Olá toouse de tamanho da máquina virtual de saudação.
   3. Insira um nome para o administrador de saudação em Olá **nome de usuário** campo. Guarde essa senha de nome e hello que entrará em seguida, você usará-los quando você fazer logon remotamente na máquina virtual de toohello.
   4. Digite uma senha na Olá **nova senha** campo e insira-a novamente no hello **confirmar** campo. Isso é a senha da conta de administrador hello.
   5. Clique em **Avançar**.
6. Em Olá próximo **configuração de máquina Virtual** caixa de diálogo:
   1. Para **serviço de nuvem**, use o padrão de saudação **criar um novo serviço de nuvem**.
   2. Olá valor **nome DNS do serviço de nuvem** devem ser exclusivas em c. Se necessário, modifique esse valor para que o Azure indique que ele é exclusivo.
   3. Especifique uma região, um grupo de afinidade ou uma rede virtual. Para o objetivo deste tutorial, especifique uma região, como **Oeste dos Estados Unidos**.
   4. Para **Conta de Armazenamento**, selecione **Usar uma conta de armazenamento gerada automaticamente**.
   5. Para **Conjunto de Disponibilidade**, selecione **(Nenhum)**.
   6. Clique em **Avançar**.
7. No final da saudação **configuração de máquina Virtual** caixa de diálogo:
   1. Aceite entradas de ponto de extremidade padrão hello.
   2. Clique em **Concluído**.

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a>log tooremotely na máquina virtual de tooyour
1. Faça logon no toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Clique em **Máquinas Virtuais**.
3. Clique Olá nome da máquina virtual Olá que você deseja toolog no.
4. Clique em **Conectar**.
5. Responda toohello prompts como máquina de virtual toohello tooconnect necessários. Quando solicitado para Olá administrador nome e senha, use valores hello fornecida quando você criou a máquina virtual de saudação.

Observe que Olá funcionalidade do barramento de serviço do Azure requer Olá Baltimore CyberTrust Root certificado toobe instalado como parte do seu JRE **cacerts** armazenar. Esse certificado é incluído automaticamente em Olá Java Runtime Environment (JRE) usado por este tutorial. Se você não tem esse certificado em seu JRE **cacerts** de armazenamento, consulte [adicionando um toohello certificado repositório de certificados de autoridade de certificação de Java] [ add_ca_cert] para obter informações sobre como adicioná-lo (bem como informações sobre como visualizar certificados Olá em seu repositório cacerts).

## <a name="how-toocreate-a-service-bus-namespace"></a>Como o namespace de barramento toocreate um serviço
filas de toobegin usando o barramento de serviço no Azure, você deve primeiro criar um namespace de serviço. Um namespace de serviço fornece um contêiner de controle para endereçamento dos recursos do Barramento de Serviço em seu aplicativo.

toocreate um namespace de serviço:

1. Faça logon no toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. No painel de navegação inferior esquerda Olá de saudação portal clássico do Azure, clique **barramento de serviço, controle de acesso e cache**.
3. No painel superior esquerdo de saudação do hello portal clássico do Azure, clique em Olá **Service Bus** nó e, em seguida, clique em Olá **novo** botão.  
   ![Captura de tela do nó do Service Bus][svc_bus_node]
4. Em Olá **criar um novo Namespace de serviço** caixa de diálogo, digite um **Namespace**, e, em seguida, clique em toomake-se de que ele seja exclusivo, o **Verificar disponibilidade** botão.  
   ![Criar uma captura de tela do novo Namespace][create_namespace]
5. Depois de verificar se o nome do namespace hello está disponível, escolha o país ou região em que o namespace deve ser hospedado e, em seguida, clique em Olá **criar Namespace** botão.  
   
   Olá namespace criado será exibida no portal clássico do Azure de saudação e entra em um momento tooactivate. Aguarde até que o status de saudação **Active** antes de continuar com a próxima etapa de saudação.

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a>Obter Olá gerenciamento de credenciais padrão para o namespace de saudação
Em operações de gerenciamento de tooperform ordem, como a criação de uma fila, no novo namespace de hello, você precisa ter credenciais de gerenciamento de saudação do tooobtain para o namespace.

1. No painel de navegação esquerdo hello, clique em Olá **Service Bus** nó para exibir a lista de saudação de namespaces disponíveis.
   ![Captura de tela de namespaces disponíveis][avail_namespaces]
2. Selecione o namespace de saudação que você acabou de criar na lista Olá mostrada.
   ![Captura de tela da lista de namespaces][namespace_list]
3. Olá direito **propriedades** painel lista as propriedades de saudação para o novo namespace.
   ![Captura de tela do painel Propriedades][properties_pane]
4. Olá **chave padrão** está oculto. Clique em Olá **exibição** botão credenciais de segurança toodisplay hello.
   ![Captura de tela da chave padrão][default_key]
5. Anote Olá **emissor padrão** e hello **chave padrão** como você usará essas informações abaixo tooperform operações com o namespace.

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a>Como toocreate um aplicativo Java que executa uma tarefa de computação intensa
1. No computador de desenvolvimento (que não tem a máquina virtual do toobe Olá que você criou), download Olá [SDK do Azure para Java](https://azure.microsoft.com/develop/java/).
2. Crie um aplicativo de console de Java usando o código de exemplo hello final Olá desta seção. Neste tutorial, vamos usar **TSPSolver.java** como nome de arquivo hello Java. Modificar Olá **sua\_service\_barramento\_namespace**, **sua\_service\_barramento\_proprietário**e **seu\_service\_barramento\_chave** toouse de espaços reservados para o barramento de serviço **namespace**, **emissor padrão** e  **Chave padrão** valores, respectivamente.
3. Depois de codificar, exportação Olá aplicativo tooa executável JAR (Java archive) e saudação de pacote necessários bibliotecas em Olá gerado JAR. Neste tutorial, vamos usar **TSPSolver.jar** como nome do JAR Olá gerado.

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a>Como toocreate um aplicativo Java que monitora Olá progresso da tarefa de computação intensiva Olá
1. No computador de desenvolvimento, crie um aplicativo de console Java usando o código de exemplo hello final Olá desta seção. Neste tutorial, vamos usar **TSPClient.java** como nome de arquivo hello Java. Como mostrado anteriormente, modificar Olá **sua\_serviço\_barramento\_namespace**, **sua\_service\_barramento\_proprietário**, e **seu\_service\_barramento\_chave** toouse de espaços reservados para o barramento de serviço **namespace**, **emissor padrão**e **chave padrão** valores, respectivamente.
2. Exportar Olá aplicativo tooa executável JAR e saudação de pacote necessários bibliotecas em Olá gerado JAR. Neste tutorial, vamos usar **TSPClient.jar** como nome do JAR Olá gerado.

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a>Como toorun Olá aplicativos Java
Executar aplicativos de computação intensiva hello, primeira fila de saudação toocreate, em seguida, toosolve Olá problema Saleseman viajando, que adicionará Olá atual melhor rota toohello fila do service bus. Durante a saudação aplicativos de computação intensiva está em execução (ou posteriormente), execução Olá cliente toodisplay resulta da fila do barramento de serviço hello.

### <a name="toorun-hello-compute-intensive-application"></a>aplicativos de computação intensiva Olá toorun
1. Faça logon na máquina virtual de tooyour.
2. Crie uma pasta onde você executará seu aplicativo. Por exemplo, **c:\TSP**.
3. Cópia **TSPSolver.jar** muito**c:\TSP**,
4. Crie um arquivo chamado **c:\TSP\cities.txt** com hello conteúdo a seguir.
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. Em um prompt de comando, altere os diretórios tooc:\TSP.
6. Verifique a pasta bin de saudação do JRE é na variável de ambiente PATH hello.
7. Você precisará fila do barramento de serviço toocreate Olá antes de executar permutações de solver TSP hello. Execute Olá fila do barramento de serviço do comando toocreate Olá a seguir.
   
        java -jar TSPSolver.jar createqueue
8. Agora que hello fila é criada, você pode executar permutações de solver TSP hello. Por exemplo, execute Olá solver de saudação do comando toorun para cidades de 8 a seguir.
   
        java -jar TSPSolver.jar 8
   
   Se você não especificar um número, ele será executado para 10 cidades. Como solver Olá localiza rotas menores atuais, ele adicionará toohello fila.

> [!NOTE]
> Olá maior Olá número que você especificar, mais solver de Olá Olá será executado. Por exemplo, a execução de 14 cidades pode levar vários minutos, e a execução de 15 cidades pode levar várias horas. Aumentando too16 ou cidades mais pode resultar em dias de tempo de execução (eventualmente semanas, meses e anos). Isso é devido toohello rápido aumento no número de saudação de permutações avaliada pelo solver hello como Olá aumento do número de cidades.
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a>Como toorun Olá monitoramento do aplicativo cliente
1. Faça logon na máquina tooyour onde você executa o aplicativo de cliente hello. Não é necessário toobe Olá mesma máquina executando Olá **TSPSolver** aplicativo, embora ele possa ser.
2. Crie uma pasta onde você executará seu aplicativo. Por exemplo, **c:\TSP**.
3. Cópia **TSPClient.jar** muito**c:\TSP**,
4. Verifique a pasta bin de saudação do JRE é na variável de ambiente PATH hello.
5. Em um prompt de comando, altere os diretórios tooc:\TSP.
6. Execute Olá comando a seguir.
   
        java -jar TSPClient.jar
   
    Opcionalmente, especifique o número de saudação de toosleep minutos entre a verificação de fila hello, passando um argumento de linha de comando. Olá período de espera padrão para a verificação de fila de saudação é 3 minutos, que é usado se nenhum argumento de linha de comando é passado muito**TSPClient**. Se você quiser toouse um valor diferente para o intervalo de suspensão de saudação, por exemplo, um minuto, execute Olá comando a seguir.
   
        java -jar TSPClient.jar 1
   
    cliente Olá será executado até que ele vê uma mensagem da fila de "Completo". Observe que, se você executar várias ocorrências do solver Olá sem executar o cliente hello, talvez seja necessário cliente de saudação toorun fila de saudação vazio toocompletely várias vezes. Como alternativa, você pode excluir fila hello e, em seguida, crie-o novamente. fila de Olá toodelete, execute o seguinte de saudação **TSPSolver** (não **TSPClient**) comando.
   
        java -jar TSPSolver.jar deletequeue
   
    o solver Olá será executado até terminar de examinar todas as rotas.

## <a name="how-toostop-hello-java-applications"></a>Como toostop Olá aplicativos Java
Para o solver hello e aplicativos cliente, você pode pressionar **Ctrl + C** tooexit se você quiser tooend toonormal anterior conclusão.

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
