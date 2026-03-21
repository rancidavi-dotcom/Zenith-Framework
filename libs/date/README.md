# date — Zenith Library

Biblioteca de data e hora para Snask, baseada no timestamp Unix do `time()`.

## Instalação

```bash
# O arquivo date.snask já está em ~/.snask/packages/
```

## Uso

```snask
import "date";

let ts = date::now();
// 1742560461 (timestamp unix)

let stamp = date::stamp();
// "[2026-03-21 12:54:21]"

let label = date::label();
// "Sabado, 21/03/2026"

let elapsed = date::since(ts_anterior);
// "3 segundos atras"
```

## Funções

| Função | Descrição |
|---|---|
| `date::now()` | Retorna timestamp Unix atual (float) |
| `date::stamp()` | String formatada `[YYYY-MM-DD HH:MM:SS]` |
| `date::label()` | Data legível em português |
| `date::since(ts)` | Tempo decorrido como string ("3s atrás") |
| `date::diff(ts1, ts2)` | Diferença em segundos entre dois timestamps |

## Observações (Snask pre-alpha)
- `date::stamp()` e `date::label()` são aproximações usando divisão inteira do Unix timestamp
- Sem suporte a fusos horários
- Baseado no horário do sistema via `time()` nativo
