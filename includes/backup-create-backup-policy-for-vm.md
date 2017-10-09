## <a name="defining-a-backup-policy"></a>Definindo uma política de backup
Uma política de backup define uma matriz de quando os instantâneos de dados de saudação são obtidos, e por quanto tempo os instantâneos são mantidos. Ao definir uma política para fazer backup de uma VM, você pode disparar um trabalho de backup *uma vez por dia*. Quando você cria uma nova política, é aplicada toohello cofre. interface de política de backup Olá tem esta aparência:

![Política do backup](./media/backup-create-policy-for-vms/backup-policy.png)

uma política de toocreate:

1. Insira um nome para Olá **nome da política**.
2. Podem ser feitos instantâneos dos dados em intervalos Diários ou Semanais. Saudação de uso **frequência de Backup** toochoose do menu suspenso se os instantâneos de dados são criados diariamente ou semanalmente.
   
   * Se você escolher intervalos diários, use Olá realçado controle tooselect Olá horário Olá para instantâneo de saudação. hora de saudação toochange, desmarque hora hello e selecione Olá nova hora.
     
     ![Política de backup diário](./media/backup-create-policy-for-vms/backup-policy-daily.png) <br/>
   * Se você escolher um intervalo semanal, use Olá controles realçado tooselect Olá dia (s) da semana hello e tempo de saudação do instantâneo de saudação do dia tootake. No menu de dia de saudação, selecione um ou vários dias. No menu de hora hello, selecione uma hora. hora de saudação toochange, desmarque hora selecionada hello e selecione Olá nova hora.
     
     ![Política de backup semanal](./media/backup-create-policy-for-vms/backup-policy-weekly.png)
3. Por padrão, todas as opções de **Intervalo de Retenção** estão selecionadas. Desmarque qualquer limite de intervalo de retenção que você deseja toouse não. Em seguida, especifique Olá interval(s) toouse.
   
    Intervalos de retenção mensal e anual permitem instantâneos de saudação toospecify com base em um incremento semanal ou diário.
   
   > [!NOTE]
   > Ao proteger uma VM, um trabalho de backup é executado uma vez por dia. tempo de saudação quando executa backup Olá é hello mesmo para cada período de retenção.
   > 
   > 
4. Depois de definir todas as opções de política hello, na parte superior de saudação da folha de saudação clique **salvar**.
   
    nova política de saudação é aplicada imediatamente toohello cofre.

