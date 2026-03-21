# str — Zenith Library

Helpers de string que complementam os builtins nativos do Snask.

## Instalação

```bash
# O arquivo str.snask já está em ~/.snask/packages/
```

## Uso

```snask
import "str";

let padded = str::pad_left("42", 5, "0");
// "00042"

let line = str::repeat("-", 30);
// "------------------------------"

let ok = str::is_empty("  ");
// true

let result = str::template("Ola, {nome}! Voce tem {n} msgs.", "nome", "David", "n", "3");
// "Ola, David! Voce tem 3 msgs."
```

## Funções

| Função | Descrição |
|---|---|
| `str::pad_left(s, n, char)` | Preenche à esquerda com `char` até tamanho `n` |
| `str::pad_right(s, n, char)` | Preenche à direita com `char` até tamanho `n` |
| `str::repeat(s, n)` | Repete a string `n` vezes |
| `str::is_empty(s)` | Retorna true se string for vazia ou só espaços |
| `str::truncate(s, n)` | Corta a string em `n` chars, adiciona `...` |
| `str::slugify(s)` | Converte para snake_case simples |

## Observações (Snask pre-alpha)
- `template()` substituição básica por pares chave/valor
- Sem suporte a regex nativo ainda
