# logger — Zenith Library

Biblioteca de logging com níveis e timestamp para Snask.

## Instalação

```bash
# O arquivo logger.snask já está em ~/.snask/packages/
```

## Uso

```snask
import "logger";

logger::info("Servidor iniciado na porta 8080");
logger::warn("Conexao com banco de dados lenta");
logger::error("Falha critica no modulo X");
logger::debug("Valor de retorno: 42");
```

## Saída

```
[INFO]  2026-03-21 12:54 | Servidor iniciado na porta 8080
[WARN]  2026-03-21 12:54 | Conexao com banco de dados lenta
[ERROR] 2026-03-21 12:54 | Falha critica no modulo X
[DEBUG] 2026-03-21 12:54 | Valor de retorno: 42
```

## Funções

| Função | Descrição |
|---|---|
| `logger::info(msg)` | Log de informação (verde em terminais que suportam) |
| `logger::warn(msg)` | Log de aviso |
| `logger::error(msg)` | Log de erro |
| `logger::debug(msg)` | Log de debug |
| `logger::raw(level, msg)` | Log com nível personalizado |

## Observações (Snask pre-alpha)
- Timestamp usa `time()` em segundos Unix
- Formatação humana é aproximada (sem biblioteca de data real ainda)
- Compatível com Zenith Framework e apps standalone
