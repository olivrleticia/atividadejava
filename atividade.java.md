# atividadejava

// Pessoa.java
public abstract class Pessoa {
    private String nome;
    private int idade;
    private String cpf;

    public Pessoa(String nome, int idade, String cpf) {
        this.nome = nome;
        this.idade = idade;
        this.cpf = cpf;
    }

    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public int getIdade() {
        return idade;
    }

    public void setIdade(int idade) {
        this.idade = idade;
    }

    public String getCpf() {
        return cpf;
    }

    public void setCpf(String cpf) {
        this.cpf = cpf;
    }

    public abstract void exibirDados();

    @Override
    public String toString() {
        return "Pessoa{" +
                "nome='" + nome + '\'' +
                ", idade=" + idade +
                ", cpf='" + cpf + '\'' +
                '}';
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;

        Pessoa pessoa = (Pessoa) o;

        return cpf.equals(pessoa.cpf);
    }

    @Override
    public int hashCode() {
        return cpf.hashCode();
    }
}

// Aluno.java
public class Aluno extends Pessoa {
    private String matricula;
    private String curso;
    private double mediaNotas; // atributo extra

    public Aluno(String nome, int idade, String cpf, String matricula, String curso, double mediaNotas) {
        super(nome, idade, cpf);
        this.matricula = matricula;
        this.curso = curso;
        this.mediaNotas = mediaNotas;
    }

    public String getMatricula() {
        return matricula;
    }

    public void setMatricula(String matricula) {
        this.matricula = matricula;
    }

    public String getCurso() {
        return curso;
    }

    public void setCurso(String curso) {
        this.curso = curso;
    }

    public double getMediaNotas() {
        return mediaNotas;
    }

    public void setMediaNotas(double mediaNotas) {
        this.mediaNotas = mediaNotas;
    }

    public String avaliarDesempenho() {
        if (mediaNotas >= 7) return "Aprovado";
        else return "Reprovado";
    }

    @Override
    public void exibirDados() {
        System.out.println("Aluno: " + getNome() + ", idade: " + getIdade() + ", CPF: " + getCpf() +
                ", Matrícula: " + matricula + ", Curso: " + curso + ", Média: " + mediaNotas +
                ", Desempenho: " + avaliarDesempenho());
    }
}

// Professor.java
public class Professor extends Pessoa {
    private String siape;
    private String disciplina;

    public Professor(String nome, int idade, String cpf, String siape, String disciplina) {
        super(nome, idade, cpf);
        this.siape = siape;
        this.disciplina = disciplina;
    }

    public String getSiape() {
        return siape;
    }

    public void setSiape(String siape) {
        this.siape = siape;
    }

    public String getDisciplina() {
        return disciplina;
    }

    public void setDisciplina(String disciplina) {
        this.disciplina = disciplina;
    }

    @Override
    public void exibirDados() {
        System.out.println("Professor: " + getNome() + ", idade: " + getIdade() + ", CPF: " + getCpf() +
                ", SIAPE: " + siape + ", Disciplina: " + disciplina);
    }
}

// TecnicoAdministrativo.java
public class TecnicoAdministrativo extends Pessoa {
    private String setor;
    private String cargo;

    public TecnicoAdministrativo(String nome, int idade, String cpf, String setor, String cargo) {
        super(nome, idade, cpf);
        this.setor = setor;
        this.cargo = cargo;
    }

    public String getSetor() {
        return setor;
    }

    public void setSetor(String setor) {
        this.setor = setor;
    }

    public String getCargo() {
        return cargo;
    }

    public void setCargo(String cargo) {
        this.cargo = cargo;
    }

    @Override
    public void exibirDados() {
        System.out.println("Técnico-Administrativo: " + getNome() + ", idade: " + getIdade() +
                ", CPF: " + getCpf() + ", Setor: " + setor + ", Cargo: " + cargo);
    }
}

// Main.java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Aluno aluno = new Aluno("Joana Silva", 21, "12345678900", "20231234", "Engenharia", 8.5);
        Professor professor = new Professor("Carlos Lima", 45, "98765432100", "56789", "Matemática");
        TecnicoAdministrativo tecnico = new TecnicoAdministrativo("Marcos Souza", 38, "11223344556", "Biblioteca", "Auxiliar");

        int soma = 0;
        for (char c : aluno.getMatricula().toCharArray()) {
            if (Character.isDigit(c)) {
                soma += Character.getNumericValue(c);
            }
        }
        int modulo = soma % 3;

        System.out.println("Soma dos dígitos da matrícula: " + soma);
        System.out.println("Estrutura escolhida (mod 3): " + modulo);

        switch (modulo) {
            case 0:
                List<Pessoa> lista = new ArrayList<>();
                lista.add(aluno);
                lista.add(professor);
                lista.add(tecnico);
                for (Pessoa p : lista) {
                    p.exibirDados();
                    System.out.println(p.toString());
                }
                break;
            case 1:
                Set<Pessoa> conjunto = new HashSet<>();
                conjunto.add(aluno);
                conjunto.add(professor);
                conjunto.add(tecnico);
                for (Pessoa p : conjunto) {
                    p.exibirDados();
                    System.out.println(p.toString());
                }
                break;
            case 2:
                Map<String, Pessoa> mapa = new HashMap<>();
                mapa.put(aluno.getCpf(), aluno);
                mapa.put(professor.getCpf(), professor);
                mapa.put(tecnico.getCpf(), tecnico);
                for (Pessoa p : mapa.values()) {
                    p.exibirDados();
                    System.out.println(p.toString());
                }
                break;
        }
    }
}
