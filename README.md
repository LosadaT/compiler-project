# Compilador Pascal-like

Trabalho desenvolvido para a disciplina de Compiladores, implementando um compilador para uma linguagem semelhante a Pascal. O projeto foi construído em C e cobre as fases de análise léxica, análise sintática e geração de código intermediário em MEPA.

## Funcionalidades

- Analisador léxico com reconhecimento de identificadores, números (decimal e notação exponencial), comentários e todos os operadores da linguagem
- Analisador sintático descendente recursivo (ASDR) baseado na gramática da linguagem
- Tabela de símbolos com hash para gerenciamento de variáveis declaradas
- Geração de código intermediário em MEPA
- Detecção de erros léxicos, sintáticos e semânticos com indicação de linha

## Estrutura do Projeto

```
.
├── compilador.c       # Código-fonte principal
├── codigo.txt         # Arquivo de entrada (código-fonte a compilar)
└── README.md
```

## Como Compilar

```bash
gcc -Wall -Wno-unused-result -g -Og compilador.c -o compilador
```

## Como Executar

O compilador lê o arquivo `codigo.txt` por padrão. Coloque o código-fonte Pascal-like nesse arquivo e execute:

```bash
./compilador
```

Para alterar o arquivo de entrada, modifique a linha 138 do `compilador.c`:

```c
FILE *f = fopen("seuarquivo.txt", "r");
```

A saída é o código MEPA gerado, impresso no terminal, seguido da tabela de símbolos ao final da execução.

## Exemplo de Entrada

```pascal
(*
programa calcula o fatorial de um numero lido
*)
program fatorial;
var
  fat, num, cont : integer;
begin
  read(num);
  fat := 1;
  cont := 2;
  while cont <= num do
  begin
    fat := fat * cont;
    cont := cont + 1
  end;
  write(fat) (*imprime o fatorial calculado*)
end.
```

## Exemplo de Saída (MEPA)

```
    INPP
    AMEM 3
    LEIT
    ARMZ 1
    CRCT 1
    ARMZ 0
    CRCT 2
    ARMZ 2
L1: NADA
    CRVL 2
    CRVL 1
    CMEG
    DSVF L2
    CRVL 0
    CRVL 2
    MULT
    ARMZ 0
    CRVL 2
    CRCT 1
    SOMA
    ARMZ 2
    DSVS L1
L2: NADA
    CRVL 0
    IMPR
    PARA

TABELA DE SIMBOLOS
Entrada Tabela Simbolos: [...] => fat | Endereco: 0
Entrada Tabela Simbolos: [...] => num | Endereco: 1
Entrada Tabela Simbolos: [...] => cont | Endereco: 2
```

## Linguagem Suportada

A gramática da linguagem é semelhante a Pascal, com suporte a:

- Tipos: `integer`, `boolean`, `char` (char ignorado na geração de código desta versão)
- Comandos: atribuição, `read`, `write`, `if/then/else`, `while/do`, blocos `begin/end`
- Operadores relacionais: `<`, `<=`, `>`, `>=`, `=`, `<>`
- Operadores lógicos: `or`, `and`, `not`
- Operadores aritméticos: `+`, `-`, `*`, `div`
- Comentários: `(* ... *)`

## Limitações Conhecidas

- O tipo `char` é reconhecido pelo léxico mas ignorado na geração de código
- Expressões mistas entre tipos (ex: `25 + (x > y)`) não geram erro semântico adequado
- Comentários não fechados retornam erro de `[END]` em vez de indicar o comentário aberto

## Tecnologias

- **C**
- **GCC**
- **MEPA** (Máquina de Execução Para Algoritmos) — linguagem de código intermediário
