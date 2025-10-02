# Mini-Lang (Python)

Analisador **léxico** + **parser LL(1)** em Python para uma mini-linguagem.
`main` e `print` são **identificadores**, não keywords. Suporta **funções** `nome(){...}`, **declarações**, **atribuições**, **if/else**, **while**, expressões aritméticas/lógicas e impressão da **AST** em ASCII.

## Como rodar

```bash
python mini_lang.py                # usa o DEMO_SOURCE interno
python mini_lang.py programa.ml    # lê de arquivo
python mini_lang.py -              # lê do stdin
```

## Exemplo de código

```txt
main() {
  int x = 10;
  soma() { print(x); }
  if (x > 5) { print(x); } else { x = x - 1; }
  soma();
}
```

## Saídas geradas

* **Tabela de Lexemas/Tokens** (com linha/coluna e `EOF`)
* **Cadeia de tokens**
* **Validação sintática** (OK/erro com posição)
* **AST** em ASCII

## Gramática (resumo)

```
program  ::= 'main' '(' ')' block
block    ::= '{' {decl} {stmt} '}'
decl     ::= ('int'|'bool') IDENT ('=' expr)? ';'
stmt     ::= if | while | assign ';' | call ';' | func | block
func     ::= IDENT '(' ')' block
call     ::= IDENT '(' [expr {',' expr}] ')'
expr     ::= ... (||, &&, ==, <, +, *, unário, primário)
```

## Mudanças recentes

* **Funções**: `IDENT () { ... }` (declaração) e `IDENT(args?);` (chamada).
* **`print` e `main`**: agora são `IDENT`; `program()` espera `IDENT 'main'`.

## Observação (Jupyter)

Se a tabela parecer "cortada", é truncamento do **Jupyter**. Ative **scroll** na saída da célula; não é necessário mudar o código.
