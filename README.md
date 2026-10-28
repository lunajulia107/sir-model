# 🦠 sir-model

**Simulação do Modelo Epidemiológico SIR** (*Susceptible, Infected, Recovered*), implementada em Java com **autômato celular** e gráficos gerados pela biblioteca **XChart**. Um desafio da faculdade que permite visualizar a propagação de uma doença em uma população ao longo do tempo.

![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![XChart](https://img.shields.io/badge/XChart-3.8.8-4A6CF7?style=flat-square)
![POO](https://img.shields.io/badge/paradigma-POO-8B53FE?style=flat-square)
![Licença MIT](https://img.shields.io/badge/licen%C3%A7a-MIT-green?style=flat-square)

[Sobre](#-sobre-o-projeto) · [Como funciona](#-como-a-simulação-funciona) · [Tecnologias](#-tecnologias-utilizadas) · [Como executar](#%EF%B8%8F-como-executar-o-projeto) · [Configurações](#-configurações) · [Créditos](#-créditos-do-projeto)

---

## Em resumo

| | |
| --- | --- |
| **O que é** | Simulação da propagação de uma doença com o modelo SIR |
| **Como** | Autômato celular em uma grade de 200 x 200 células, por 100 iterações |
| **Resultado** | Gráfico de linhas com suscetíveis, infectados e recuperados ao longo do tempo |
| **Linguagem** | Java, com Programação Orientada a Objetos |
| **Base teórica** | Artigo em `artigo_sir.pdf` |
| **Tipo** | Desafio da faculdade, feito em equipe |

---

## 📌 Sobre o projeto

🧮 O modelo SIR é amplamente utilizado em epidemiologia para representar a dinâmica de surtos e epidemias. Este sistema simula a evolução do número de suscetíveis, infectados e recuperados, exibindo resultados gráficos para facilitar a análise.

O projeto foi desenvolvido em Java, utilizando programação orientada a objetos, e faz uso da biblioteca **XChart** para exibição de gráficos interativos.

> [!NOTE]
> O desafio pedia para simular o modelo SIR com autômato celular em um reticulado de 200 x 200 por 100 iterações, chegando a um gráfico de linhas igual à figura 3 do artigo.

---

## 🔬 Como a simulação funciona

Cada célula da grade representa um indivíduo e pode estar em um de três estados:

| Estado | Significado |
| --- | --- |
| 🟦 **S** · Suscetível | Pode ser infectado |
| 🟥 **I** · Infectado | Está doente e pode contaminar os vizinhos |
| 🟩 **R** · Recuperado | Se recuperou da doença |

A simulação começa com **todas as células suscetíveis e uma infectada no centro**. A cada iteração, as células mudam de estado de acordo com estas regras:

| Transição | Regra |
| --- | --- |
| **S → I** | Probabilidade `1 - e^(-k · v)`, onde `k = 1` e `v` é o número de vizinhos infectados |
| **S → R** | Probabilidade constante |
| **I → R** | Probabilidade constante de 60% |
| **I → S** | Probabilidade constante de 30% |
| **R → S** | Probabilidade constante de 10% |

No fim, o gráfico mostra a proporção de cada estado em relação à população total.

---

## 🛠 Tecnologias utilizadas

| Tecnologia | Para que serve |
| --- | --- |
| **Java** | Linguagem da simulação |
| **XChart (v3.8.8)** | Biblioteca gráfica para gerar o gráfico de linhas |
| **POO** | Paradigma usado para organizar as classes |

### 🧩 Classes

| Classe | Responsabilidade |
| --- | --- |
| `Main` | Ponto de entrada da aplicação |
| `Simulacao` | Controla os parâmetros, executa as iterações e gera o gráfico |
| `AutomatoCelular` | Lógica do autômato: grade, regras de transição e contagem de vizinhos |
| `Celula` | Representa cada célula/indivíduo da simulação |

A pasta `resume/` tem um resumo explicando cada classe e os conceitos de Java usados.

---

## ⚙️ Como executar o projeto

**Requisitos:**

- Java Development Kit (JDK) instalado (versão 8 ou superior recomendada)
- Biblioteca XChart disponível na pasta `lib/`

### 1️⃣ Clonar o repositório

```bash
git clone https://github.com/lunajulia107/modeloSIR.git
cd modeloSIR
```

### 2️⃣ Compilar o projeto

Abra o terminal na pasta do projeto e execute:

**No Windows**

```bash
javac -cp ".;lib/xchart-3.8.8.jar" *.java
```

**No Linux ou macOS**

```bash
javac -cp ".:lib/xchart-3.8.8.jar" *.java
```

### 3️⃣ Executar o programa

**No Windows**

```bash
java -cp ".;lib/xchart-3.8.8.jar" Main
```

**No Linux ou macOS**

```bash
java -cp ".:lib/xchart-3.8.8.jar" Main
```

Uma janela abre com o gráfico da simulação. 📈

---

## 🎛 Configurações

Os parâmetros da simulação ficam em `Main.java`, na criação da `Simulacao`:

```java
Simulacao simulacao = new Simulacao(200, 1, 15, 100);
```

| Posição | Parâmetro | Valor atual | O que define |
| --- | --- | --- | --- |
| 1º | `tamanho` | `200` | Tamanho da grade (200 x 200 células) |
| 2º | `taxaInfeccao` | `1` | Taxa de infecção |
| 3º | `tempoRecuperacao` | `15` | Tempo de recuperação |
| 4º | `iteracoes` | `100` | Número de passos da simulação |

As probabilidades de cada transição ficam no método `aplicarRegras`, em `AutomatoCelular.java`.

Após alterar, compile e execute novamente.

---

## 📦 Dependências

- A biblioteca XChart está na pasta `lib/xchart-3.8.8.jar`
- Caso precise baixar a biblioteca, acesse: [knowm.org/open-source/xchart](https://knowm.org/open-source/xchart/)

---

## 📁 Estrutura do projeto

```
modeloSIR/
├── lib/                      → dependências externas
│   └── xchart-3.8.8.jar      → biblioteca para geração de gráficos
├── resume/                   → resumo em relação a cada classe
├── AutomatoCelular.java      → lógica do autômato para simulação
├── Celula.java               → representa cada célula/indivíduo da simulação
├── Main.java                 → ponto de entrada da aplicação
├── Simulacao.java            → controla os parâmetros e execução da simulação
└── artigo_sir.pdf            → documento explicativo sobre o modelo SIR
```

---

## 🤝 Créditos do projeto

| Área | Responsável |
| --- | --- |
| 🧩 Apoio na lógica e entendimento | Julia Gomes |
| 🤝 Entendimento do problema | Camila Bonilha |
| 🎤 Apresentação | Samara Duarte |

✉️ Para dúvidas ou sugestões, entre em contato: [rodriguesjuliaw23@gmail.com](mailto:rodriguesjuliaw23@gmail.com)

---

## 📄 Licença

Este projeto está sob a licença **MIT**.
