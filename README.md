# Zenith Framework - A Laravel-Inspired Framework for Snask

## 🚀 Introdução ao Zenith

**Zenith** é um framework ambicioso para o ecossistema Snask, projetado para trazer a elegância, a produtividade e a experiência de desenvolvimento robusta inspiradas no Laravel para o mundo das aplicações desktop e de linha de comando construídas com Snask.

Em um cenário onde Snask se destaca pela performance e pelo foco em tooling, Zenith visa fornecer uma estrutura organizada e opinionada que capacita desenvolvedores a construir aplicações complexas de forma mais eficiente e agradável. A inspiração no Laravel é traduzida em princípios como:

*   **Experiência do Desenvolvedor (DX):** Ferramentas CLI intuitivas, convenções claras e feedback útil.
*   **Estrutura Organizada:** Uma arquitetura que promove a separação de responsabilidades (MVC-like, adaptado para Snask).
*   **Componentização:** Um sistema de container para gerenciamento de dependências e serviços.
*   **Produtividade:** Facilidade na criação de componentes comuns (comandos, interações com banco de dados, configuração).

Zenith não é apenas um conjunto de bibliotecas, mas uma filosofia para construir aplicações Snask de maneira escalável, manutenível e prazerosa.

## ✨ Visão e Objetivos Principais

A visão do Zenith é ser a escolha padrão para o desenvolvimento de aplicações mais elaboradas em Snask, sejam elas:

*   **Ferramentas de Linha de Comando (CLI):** Da mais simples utilidade à automação complexa.
*   **Aplicações Desktop:** Aproveitando o suporte a GUI do Snask (inicialmente via GTK) para criar interfaces gráficas ricas.
*   **Serviços e Backends:** Embora focado em desktop/CLI, a estrutura permitirá a criação de APIs ou serviços de fundo.

Os objetivos principais para o Zenith incluem:

*   **Abstração e Facilidade:** Simplificar tarefas comuns através de abstrações de alto nível.
*   **Performance:** Alavancar a performance nativa do Snask, garantindo que o framework não se torne um gargalo.
*   **Testabilidade:** Facilitar a escrita de testes para a lógica da aplicação.
*   **Ecossistema:** Sentir-se como uma extensão natural do ecossistema Snask, utilizando seus recursos como SNIF, SPS e as bibliotecas nativas.

## 🗺️ Plano de Desenvolvimento Detalhado

Este plano descreve as etapas para o desenvolvimento inicial do Zenith Framework.

### Fase 1: Fundamentos do Framework (`zenith-core`)

O núcleo do Zenith será desenvolvido como uma biblioteca reutilizável.

#### Tarefa 1.1: Estrutura do Diretório `zenith/core/`
*   Criar o diretório `zenith/core/`.
*   Estabelecer a estrutura de arquivos para a biblioteca:
    *   `zenith/core/package.json` (Metadados da biblioteca).
    *   `zenith/core/package.snask` (Código principal da biblioteca).
    *   `zenith/core/README.md` (Documentação específica do core).

#### Tarefa 1.2: Implementar o Container de Serviços (IoC)
*   Criar `zenith/core/Container.snask`:
    *   Gerenciamento de bindings (associações nome-função/instância).
    *   Suporte para registrar serviços (`bind()`) e singletons (`singleton()`).
    *   Mecanismo para resolver serviços (`make()`).
    *   Inicialização com um `Container` simplificado.
*   Criar `zenith/core/Application.snask`:
    *   Herança ou composição com `Container`.
    *   Lógica de inicialização da aplicação (`start()`).
    *   Gerenciamento da versão do framework.
    *   Ponto de entrada para obter o container.

#### Tarefa 1.3: Desenvolver o Componente Console (`artisan`-like)
*   Criar `zenith/core/Console/Command.snask`:
    *   Classe base para comandos CLI.
    *   Definição de `name`, `description`.
    *   Método `handle()` a ser implementado pelas subclasses.
*   Criar `zenith/core/Console/Kernel.snask`:
    *   Um `Console` que gerencia uma lista de `Command`.
    *   Método `add()` para registrar comandos.
    *   Método `run()` para processar argumentos da linha de comando e despachar comandos.

#### Tarefa 1.4: Camada de Acesso a Dados (SQLite)
*   Criar `zenith/core/Database/Manager.snask`:
    *   Gerenciamento de conexões com bancos de dados (inicialmente apenas SQLite).
    *   Configuração via SNIF.
*   Criar `zenith/core/Database/Query/Builder.snask`:
    *   Um construtor de queries simplificado, similar a `DB::table('users')->get()`.
    *   Implementar métodos básicos como `table()`, `select()`, `where()`, `get()`, `first()`, `insert()`, `update()`, `delete()`.

#### Tarefa 1.5: Carregador de Configuração
*   Criar `zenith/core/Config/FileLoader.snask`:
    *   Carregar arquivos SNIF (ou outros formatos como JSON, TOML) do diretório `config/`.
    *   Fornecer acesso a configurações de forma estruturada.

### Fase 2: Esqueleto de Aplicação (`zenith-skeleton`)

O esqueleto fornecerá uma estrutura inicial para novos projetos Zenith.

#### Tarefa 2.1: Estrutura de Diretórios Padrão
*   Criar o diretório `zenith/skeleton/`.
*   Estabelecer a estrutura de arquivos:
    *   `snask.snif`: Manifest do projeto SPS.
    *   `main.snask`: Ponto de entrada principal da aplicação (inicia o framework).
    *   `zenith`: Script CLI para gerenciar a aplicação (bootstrapping).
    *   `app/`: Código da aplicação (Commands, Models, Services, etc.).
        *   `app/Console/Kernel.snask`: Registra os comandos da aplicação.
    *   `config/`: Arquivos de configuração (e.g., `app.snif`, `database.snif`).
    *   `routes/`: Definições de rotas (e.g., `console.snask` para comandos CLI).
    *   `database/`:
        *   `migrations/`: Scripts para migrações de banco de dados.
        *   `seeds/`: Scripts para popular o banco de dados.
    *   `tests/`: Testes automatizados.
    *   `resources/`: Arquivos de recursos (e.g., templates UI, assets).

#### Tarefa 2.2: Ponto de Entrada da Aplicação (`main.snask` e `zenith` script)
*   Configurar `main.snask` para inicializar a `Application` do Zenith e registrar o `Kernel` de console.
*   Criar o script `zenith` (executável) que bootstraps a aplicação e executa comandos.

### Fase 3: Ferramentas CLI e Scaffolding

Capacitar desenvolvedores a criar projetos e componentes rapidamente.

#### Tarefa 3.1: Implementar Comandos Base para o `zenith` CLI
*   Comandos como `zenith make:command`, `zenith make:model`, `zenith migrate`.
*   Integração com o `Console` component do core.

### Fase 4: Verificação e Testes

Garantir a estabilidade e a funcionalidade do framework.

#### Tarefa 4.1: Testes Unitários e de Integração
*   Escrever testes para o `Container`, `Console`, `Database` e outras partes do core.
*   Criar exemplos de uso no `zenith-skeleton` para validar o fluxo completo.

## Arquitetura e Conceitos

*   **Container (IoC):** Centraliza a configuração e o gerenciamento de serviços, permitindo injeção de dependência e fácil substituição de componentes.
*   **Console/Commands:** Um sistema robusto para a criação e execução de tarefas via linha de comando.
*   **Database Abstraction:** Abstrai as complexidades do SQLite, permitindo queries mais declarativas e legíveis.
*   **SNIF Configuration:** Utiliza o formato SNIF para configurações, aproveitando a integração nativa do Snask.
*   **SPS for Dependencies:** Gerencia dependências do framework e das aplicações construídas sobre ele via `snask.snif`.

## Próximos Passos Imediatos

1.  Finalizar a implementação do `Container` e `Application` no `zenith/core/package.snask`.
2.  Corrigir os erros de sintaxe identificados no `main.snask` (pontuação e declaração de propriedades).
3.  Criar o `zenith/skeleton/snask.snif` e `zenith/skeleton/main.snask` com as correções.
4.  Tentar compilar o esqueleto para verificar a integração com o core.

Este plano é um guia e pode evoluir à medida que o desenvolvimento avança e novas descobertas são feitas sobre as capacidades e limitações do Snask.
