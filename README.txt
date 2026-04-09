Passo 1: O Nascimento dos Dados (Veiculo)
Tudo começou com a criação da unidade básica. Você definiu que, para o sistema existir, era preciso ter um Veículo.

No main, você capturou as Strings (Placa e Modelo).

Ao fazer Veiculo veiculo = new Veiculo(placa, modelo);, você criou uma "caixinha" que guarda essas duas informações juntas. Sem isso, a placa e o modelo ficariam "soltos" e perdidos no código.

Passo 2: A Camada de Negócio (Ticket)
Aqui foi onde você conectou a primeira peça à segunda. O Ticket é quem entende de dinheiro e tempo.

Ao instanciar Ticket ticket = new Ticket(veiculo, tempoperm);, você passou o objeto veiculo inteiro para dentro do ticket.

A conexão: Agora, o Ticket não guarda apenas o tempo; ele guarda o Veículo dono daquele tempo.

O Processamento: Assim que o Ticket nasceu, o Construtor dele já gritou para o método calculaTaxa(): "Ei, faz a conta aí!". O valor foi calculado no exato momento da criação.

Passo 3: O Armazenamento Coletivo (ArrayList)
Você percebeu que, se criasse um ticket novo no while, o antigo sumiria na próxima rodada.

Você criou a ArrayList<Ticket> listaTicket.

Com o listaTicket.add(ticket);, você pegou aquele ticket (que já carregava o veículo dentro dele) e o colocou em uma "estante" organizada.

Passo 4: A Navegação Profunda (Busca e Exclusão)
Este foi o passo mais importante da lógica de Engenharia. No opc == 2 e opc == 3, você precisava achar um carro específico.

Você usou o for para percorrer a estante (ArrayList).

O "Caminho das Pedras": Para cada posição a, você fez uma viagem:

Parou no Ticket daquela posição: listaTicket.get(a)

Entrou no Veículo desse ticket: .getVeiculo()

Leu a Placa desse veículo: .getPlaca()

Comparou com o que o usuário digitou: .equals(removeplaca)

Passo 5: A Manutenção da Memória
Quando a comparação deu true, você deu a ordem listaTicket.remove(a);.

O Java, então, tirou aquele Ticket da estante. Como o Veículo estava dentro daquele Ticket, ele foi removido junto.


//////////////////////////////

1. Conversa via Parâmetro (O "Contrato Temporário")
É quando uma classe não "é dona" da outra, ela apenas recebe o objeto na hora de executar uma ação.

Exemplo: A classe Curso contrata um Professor.
O curso não nasce com um professor fixo; você "passa" o professor para o método de contratação.

Java
public class Curso {
    private String nomeCurso;

    public void contratarProfessor(Professor prof) {
        // Aqui o Curso está conversando com a classe Professor
        System.out.println("O curso " + this.nomeCurso + " contratou o prof. " + prof.getNome());
    }
}
Analogia: É como um médico atendendo um paciente. O médico não "tem" o paciente para sempre; ele recebe o paciente no consultório (parâmetro), faz o trabalho e pronto.

2. Conversa via Atributo (A "Posse" ou Composição)
É quando uma classe guarda a outra dentro dela. Foi o que você fez com Ticket e Veiculo.

Exemplo: Um Aluno tem um Curso trancado nele.
Para o aluno saber o que está estudando, ele precisa ter um atributo do tipo Curso.

Java
public class Aluno {
    private String nome;
    private Curso cursoMatriculado; // Atributo que é outra classe

    public void mostrarDados() {
        System.out.println("Aluno: " + this.nome);
        // O Aluno conversa com o Curso para saber o nome dele
        System.out.println("Estuda o curso: " + cursoMatriculado.getNomeCurso());
    }
}
3. Conversa via Lista (O "Gerenciamento")
É quando uma classe precisa listar ou interagir com vários objetos de outra classe.

Exemplo: O Professor lista seus Alunos.
O professor tem um ArrayList<Aluno>. Para "conversar" com eles, ele usa um loop.

Java
public class Professor {
    private ArrayList<Aluno> meusAlunos = new ArrayList<>();

    public void darNotaGeral() {
        for (Aluno a : meusAlunos) {
            // O Professor conversa com cada aluno da lista e executa um método dele
            a.receberNota(10.0); 
        }
    }
}
O Segredo para não errar: "Quem precisa saber de quem?"
Na Engenharia de Software, antes de codar, você faz uma pergunta: "Para eu fazer essa ação, de quais informações eu preciso?"

Se para Contratar, eu preciso saber quem é o Professor -> O método contratar deve receber (Professor p) como parâmetro.

Se para Listar Alunos, o Professor precisa ter os contatos deles -> O Professor deve ter um ArrayList<Aluno>