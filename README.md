# java-java
class Lutador {

    private String lutadorNome;
    private int lutadorDano;
    private int lutadorVida;
    private int lutadorIniciativa;

    public Lutador(String lutadorNome, int lutadorDano, int lutadorVida, int lutadorIniciativa) {
        this.lutadorNome = lutadorNome;
        this.lutadorDano = lutadorDano;
        this.lutadorVida = lutadorVida;
        this.lutadorIniciativa = lutadorIniciativa;
    }

    // Getters e Setters
    public String getLutadorNome() {
        return lutadorNome;
    }

    public int getLutadorDano() {
        return lutadorDano;
    }

    public int getLutadorVida() {
        return lutadorVida;
    }

    public int getLutadorIniciativa() {
        return lutadorIniciativa;
    }

    public static void checarStatus(Lutador[] timeEstaticoStatus, int maximo) {
        // Verificar status de cada lutador
        for (int i = 0; i < maximo; i++) {
            if (timeEstaticoStatus[i] != null) {
                System.out.printf("Status de %s: Vida = %d | Iniciativa = %d\n",
                        timeEstaticoStatus[i].getLutadorNome(),
                        timeEstaticoStatus[i].getLutadorVida(),
                        timeEstaticoStatus[i].getLutadorIniciativa());
            }
        }
    }

    public static Lutador checarRemoverLutador(Lutador[] timeEstaticoRemover, String lutadorNome, int maximo) {
        for (int i = 0; i < maximo; i++) {
            if (timeEstaticoRemover[i] != null && timeEstaticoRemover[i].getLutadorNome().equals(lutadorNome)) {
                Lutador lutadorRemovido = timeEstaticoRemover[i];
                timeEstaticoRemover[i] = null;
                return lutadorRemovido;
            }
        }
        return null;
    }
    public void sofrerDano(int danoRecebido) {
        this.lutadorVida -= danoRecebido;
        if (this.lutadorVida < 0) {
            this.lutadorVida = 0;  // Garantir que a vida não fique negativa
        }
        System.out.printf("O lutador %s sofreu %d de dano e agora tem %d de vida.\n", lutadorNome, danoRecebido, lutadorVida);
    }
}
public class CombateAtivo {

    // Método para simular o combate entre dois times
    public static void realizarCombate(Lutador[] time1, Lutador[] time2, int maximo1, int maximo2) {
        // Lógica quando Time1 tem mais ou igual lutadores do que Time2
        if (maximo1 >= maximo2) {
            for (int i = 0; i < maximo2; i++) {
                combateIndividual(time1[i], time2[i]);
            }

            // Se Time1 tem mais lutadores, o último lutador do Time1 sofre dano de todos os lutadores restantes do Time2
            if (maximo1 > maximo2) {
                for (int i = maximo2; i < maximo1; i++) {
                    for (int j = 0; j < maximo2; j++) {
                        time1[i].sofrerDano(time2[j].getLutadorDano());
                    }
                    verificarMorte(time1[i]);
                }
            }
        } else { // Caso Time2 tenha mais lutadores do que Time1
            for (int i = 0; i < maximo1; i++) {
                combateIndividual(time1[i], time2[i]);
            }

            // Se Time2 tem mais lutadores, o último lutador do Time2 sofre dano de todos os lutadores restantes do Time1
            if (maximo2 > maximo1) {
                for (int i = maximo1; i < maximo2; i++) {
                    for (int j = 0; j < maximo1; j++) {
                        time2[i].sofrerDano(time1[j].getLutadorDano());
                    }
                    verificarMorte(time2[i]);
                }
            }
        }
    }

    // Método para realizar o combate entre dois lutadores
    private static void combateIndividual(Lutador lutador1, Lutador lutador2) {
        int dano1 = lutador1.getLutadorDano();
        int dano2 = lutador2.getLutadorDano();

        // Ataque simultâneo: ambos os lutadores sofrem dano ao mesmo tempo
        lutador1.sofrerDano(dano2);  // Lutador 1 sofre dano do Lutador 2
        lutador2.sofrerDano(dano1);  // Lutador 2 sofre dano do Lutador 1

        // Verificar a morte de cada lutador após os ataques simultâneos
        verificarMorte(lutador1);
        verificarMorte(lutador2);
    }

    // Método para verificar se um lutador morreu e, se sim, mover para o cemitério
    private static void verificarMorte(Lutador lutador) {
        if (lutador.getLutadorVida() <= 0) {
            System.out.printf("O lutador %s morreu!!\n", lutador.getLutadorNome());
            Time.inserirCemiterio(cemiterio1, lutador);
        }
    }
}
class Time {

    private String nomeTime;
    private Lutador[] lutadores;
    private static final int CAPACIDADE = 10;
    public static int maximo1 = 5;
    public static int maximo2 = 5;

    public Time(String nomeTime) {
        this.nomeTime = nomeTime;
        this.lutadores = new Lutador[CAPACIDADE];
    }

    public boolean inserirLutador(Lutador lutador) {
        for (int i = 0; i < lutadores.length; i++) {
            if (lutadores[i] == null) {
                lutadores[i] = lutador;
                System.out.println("Lutador " + lutador.getLutadorNome() + " adicionado ao time " + nomeTime);
                return true; // Lutador adicionado com sucesso
            }
        }
        return false; // Time cheio
    }

    public static void inserirCemiterio(Lutador cemiterio, String lutadorNome) {
        for (int i = 0; i < cemiterio.length; i++) {
            if (cemiterio[i] == null) {
                cemiterio[i] = lutador;
                System.out.println("Lutador " + lutadorNome + " adicionado ao cemitério.");
                return;
            }
        }
        System.out.println("O cemitério está cheio!");
    }

    // Getters e setters
    public String getNomeTime() {
        return nomeTime;
    }

    public Lutador[] getLutadores() {
        return lutadores;
    }
    //funções diversas
    public static int retirarDeMax(int maximo){
        return maximo--;
    }
    public static int adicionarDeMax(int maximo){
        return maximo++;
    }
}
//TIP To <b>Run</b> code, press <shortcut actionId="Run"/> or
// click the <icon src="AllIcons.Actions.Execute"/> icon in the gutter.
/*
começando pela classe time:

- O identificador é o próprio objeto apresentado
- O código gira em torno dos objetos instanciados Time1 e Time 2, que possuem alguns atributos
- Ao final, adicionar comentários e fazer as devidas alterações necessárias
- correção na linha 340
- Há um problema no combate: se tiver menos combatentes em um do que em outro ??
- Tirar os casters (sem razão)
- Verificar aritmética de vetores
- adicionar um metodo que aumenta o tamanho do vetor time no processo de
adicionar elementos
 */



import java.util.Scanner;

import java.util.Scanner;

class Main {
    public static void main(String[] args) {
        // Criação dos times
        Time time1 = new Time("Time 1");
        Time time2 = new Time("Time 2");
        Lutador[] cemiterio1 = new Lutador[30];
        Lutador[] cemiterio2 = new Lutador[30];

        // Instanciando lutadores
        Lutador lutador1 = new Lutador("GeraltDeRivia", 90, 28, 45);
        Lutador lutador2 = new Lutador("Ciri", (int) (Math.random() * 101), (int) (Math.random() * 101), 60);
        Lutador lutador3 = new Lutador("Lambert", (int) (Math.random() * 101), (int) (Math.random() * 101), 18);
        Lutador lutador4 = new Lutador("Yennefer", (int) (Math.random() * 101), (int) (Math.random() * 101), 30);
        Lutador lutador5 = new Lutador("Vesemir", (int) (Math.random() * 101), (int) (Math.random() * 101), 57);
        Lutador lutador6 = new Lutador("Cocatriz", (int) (Math.random() * 101), (int) (Math.random() * 101), 23);
        Lutador lutador7 = new Lutador("Moira1", (int) (Math.random() * 101), (int) (Math.random() * 101), 41);
        Lutador lutador8 = new Lutador("Moira2", (int) (Math.random() * 101), (int) (Math.random() * 101), 47);
        Lutador lutador9 = new Lutador("Grifo", (int) (Math.random() * 101), (int) (Math.random() * 101), 39);
        Lutador lutador10 = new Lutador("Lobisomem", (int) (Math.random() * 101), (int) (Math.random() * 101), 21);

        time1.inserirLutador(lutador1);
        time1.inserirLutador(lutador2);
        time1.inserirLutador(lutador3);
        time1.inserirLutador(lutador4);
        time1.inserirLutador(lutador5);
        time2.inserirLutador(lutador6);
        time2.inserirLutador(lutador7);
        time2.inserirLutador(lutador8);
        time2.inserirLutador(lutador9);
        time2.inserirLutador(lutador10);

        System.out.println("Bem vindo ao RPG Tucano !!!!!");
        System.out.println("\nVamos ao jogo:\n\nTime 1:\n");

        // Imprimindo os nomes dos lutadores do time 1
        System.out.println("Time 1:");
        for (int i = 0; i < Time.maximo1; i++) {
            System.out.printf("%s", time1.getLutadores()[i].getLutadorNome());
            if ((i + 1) % 2 == 0) {
                System.out.println(); // Quebra de linha após cada par de nomes
            }
        }
        if (Time.maximo1 % 2 != 0) {
            System.out.println(); // Adiciona uma linha extra caso o número de lutadores seja ímpar
        }

        // Imprimindo os nomes dos lutadores do time 2
        System.out.println("Time 2:");
        for (int i = 0; i < Time.maximo2; i++) {
            System.out.printf("%s", time2.getLutadores()[i].getLutadorNome());
            if ((i + 1) % 2 == 0) {
                System.out.println(); // Quebra de linha após cada par de nomes
            }
        }
        if (Time.maximo2 % 2 != 0) {
            System.out.println(); // Adiciona uma linha extra caso o número de lutadores seja ímpar
        }

        System.out.println("Vamos começar? (s/n)");
        Scanner scanner = new Scanner(System.in);
        String opcao = scanner.nextLine();
        if (opcao.equals("s")) {
            do{
                System.out.println("\nDeseja dar um trato na sua equipe?");
                System.out.println("1 - Checar status de um time");
                System.out.println("2 - Remover lutador de um time");
                System.out.println("3 - Adicionar um novo lutador");
                System.out.println("0 - Sair");
                System.out.print("Opção: ");
                opcao = scanner.nextLine();

                switch (opcao) {
                    case "1":
                        System.out.println("Checar status de qual time? (1 ou 2): ");
                        int timeEscolhido = scanner.nextInt();
                        if (timeEscolhido == 1) {
                            Lutador.checarStatus(time1.getLutadores(), Time.maximo1);  // Checa o status do Time 1
                        } else if (timeEscolhido == 2) {
                            Lutador.checarStatus(time2.getLutadores(), Time.maximo2);  // Checa o status do Time 2
                        }
                        break;
                    case "2":
                        System.out.println("Digite o nome do lutador para remover: ");
                        scanner.nextLine(); // Consumir quebra de linha
                        String nomeParaRemover = scanner.nextLine();
                        System.out.println("Remover de qual time? (1 ou 2): ");
                        int timeRemover = scanner.nextInt();
                        if (timeRemover == 1) {
                            Lutador.checarRemoverLutador(time1.getLutadores(), nomeParaRemover, Time.maximo1);
                            Time.retirarDeMax(Time.maximo1);
                        } else if (timeRemover == 2) {
                            Lutador.checarRemoverLutador(time2.getLutadores(), nomeParaRemover, Time.maximo2);
                            Time.retirarDeMax(Time.maximo2);
                        }
                        break;
                    case "3": // Adicionar um novo lutador a um time
                        System.out.print("Digite o nome do lutador: ");
                        scanner.nextLine(); // Consumir quebra de linha
                        String nomeLutador = scanner.nextLine();

                        System.out.print("Digite o dano causado pelo lutador (0-100): ");
                        int lutadorDano = scanner.nextInt();

                        System.out.print("Digite a vida inicial do lutador (0-100): ");
                        int lutadorVida = scanner.nextInt();

                        System.out.print("Digite a iniciativa do lutador: ");
                        int lutadorIniciativa = scanner.nextInt();

                        // Criação do novo lutador com os dados fornecidos
                        Lutador novoLutador = new Lutador(nomeLutador, lutadorDano, lutadorVida, lutadorIniciativa);

                        // Perguntar em qual time adicionar o lutador
                        System.out.print("Adicionar o lutador ao Time 1 ou Time 2? (1 ou 2): ");
                        int timeAdicionar = scanner.nextInt();

                        boolean adicionado = false;

                        if (timeAdicionar == 1) {
                            // Adicionar ao Time 1
                            adicionado = time1.inserirLutador(novoLutador);
                            if (adicionado) {
                                Time.adicionarDeMax(Time.maximo1);
                            }
                        } else if (timeAdicionar == 2) {
                            // Adicionar ao Time 2
                            adicionado = time2.inserirLutador(novoLutador);
                            if (adicionado) {
                                Time.adicionarDeMax(Time.maximo2);
                            }
                        } else {
                            System.out.println("Time inválido! Escolha 1 ou 2.");
                        }
                        break;
                    case "0":
                        System.out.println("\n\n------------------\nCombate iniciado:\n-----------------\n\n");
                        CombateAtivo.realizarCombate(time1.getLutadores(), time2.getLutadores(), Time.maximo1, Time.maximo2);
                        break;

                    default:
                        System.out.println("Opção inválida!");
                }
                scanner.close();
                // Após o combate, chame a fase de resultados
                FaseResultados.executarFaseResultados(time1, time2, cemiterio1, cemiterio2);

            }while(!FaseResultados.continuarJogo(time1, time2));
        }
    }
}
public class FaseResultados {

    // Função que executa a fase de resultados após o combate
    public static void executarFaseResultados(Time time1, Time time2, Lutador[] cemiterio1, Lutador[] cemiterio2) {
        int scoreTime1 = calcularScore(cemiterio1);  // Calcula o score do Time 1
        int scoreTime2 = calcularScore(cemiterio2);  // Calcula o score do Time 2

        boolean time1ComLutadorVivo = verificarLutadoresVivos(time1);
        boolean time2ComLutadorVivo = verificarLutadoresVivos(time2);

        // Condição 1: Se um time tiver ao menos um lutador vivo e o adversário não
        if (time1ComLutadorVivo && !time2ComLutadorVivo) {
            System.out.println("O Time 1 venceu!");
            return;
        } else if (!time1ComLutadorVivo && time2ComLutadorVivo) {
            System.out.println("O Time 2 venceu!");
            return;
        }

        // Condição 2: Se ambos os times tiverem lutadores vivos e um time alcançar score >= 20
        if (time1ComLutadorVivo && time2ComLutadorVivo) {
            if (scoreTime1 >= 20 && scoreTime2 < 20) {
                System.out.println("O Time 1 venceu por score maior que 20!");
                return;
            } else if (scoreTime2 >= 20 && scoreTime1 < 20) {
                System.out.println("O Time 2 venceu por score maior que 20!");
                return;
            }

            // Condição 3: Se ambos os times tiverem score > 20, o time com maior score vence
            if (scoreTime1 > scoreTime2) {
                System.out.println("O Time 1 venceu por maior score!");
                return;
            } else if (scoreTime2 > scoreTime1) {
                System.out.println("O Time 2 venceu por maior score!");
                return;
            }

            // Condição 4: Se ambos os times ficaram vazios e o score for igual, empate
            if (!time1ComLutadorVivo && !time2ComLutadorVivo) {
                if (scoreTime1 == scoreTime2) {
                    System.out.println("Empate!");
                } else {
                    System.out.println("O time com maior score venceu!");
                }
                return;
            }
        }

        // Se nenhuma condição de término for atendida, o jogo continua
    }

    // Função que verifica se há lutadores vivos em um time
    private static boolean verificarLutadoresVivos(Time time) {
        for (Lutador lutador : time.getLutadores()) {
            if (lutador != null && lutador.getLutadorVida() > 0) {
                return true; // Encontrou um lutador vivo
            }
        }
        return false; // Nenhum lutador vivo encontrado
    }

    // Função que calcula o score do time, baseado na quantidade de lutadores no cemitério adversário
    private static int calcularScore(Lutador[] cemiterio) {
        int score = 0;
        for (Lutador lutador : cemiterio) {
            if (lutador != null) {
                score++;
            }
        }
        return score;
    }

    // Função que verifica se o jogo deve continuar
    public static boolean continuarJogo(Time time1, Time time2) {
        // Se ambos os times tiverem lutadores vivos, o jogo continua
        boolean time1ComLutadorVivo = verificarLutadoresVivos(time1);
        boolean time2ComLutadorVivo = verificarLutadoresVivos(time2);

        // O jogo só continuará se ambos os times tiverem lutadores vivos
        return time1ComLutadorVivo && time2ComLutadorVivo;
    }
}
