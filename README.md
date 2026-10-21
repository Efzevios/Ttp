# traduzir — tradução de saídas de terminal GNU/Linux

Tradutor de saída de comandos e páginas `man` para **português brasileiro**, executado como função Bash. Preserva, sempre que possível, comandos, opções, caminhos, URLs, estrutura e indentação.

**Motores disponíveis:** documentação localizada (`man`/gettext), APIs de IA (OpenRouter, Gemini, OpenAI, Anthropic), `translate-shell`, Apertium e Argos Translate. Inclui cache, armazenamento organizado, rotação de chaves por provedor, tratamento de falhas e proteção de termos técnicos para tradutores convencionais.

## Instalação rápida (Debian 13)

```bash
bash instalar_dependencias.sh --basico --apis
mkdir -p ~/.local/share/traduzir
cp traduzir.bash ~/.local/share/traduzir/
cp credenciais_modelos.sh.example ~/.local/share/traduzir/credenciais_modelos.sh
chmod 600 ~/.local/share/traduzir/credenciais_modelos.sh
```

Adicione ao seu `~/.bashrc`:

```bash
source "$HOME/.local/share/traduzir/traduzir.bash"
```

Recarregue com `source ~/.bashrc`. Configure as chaves no arquivo **local** `~/.local/share/traduzir/credenciais_modelos.sh` e escolha os modelos que o `llm` realmente lista.

Para instalar **todos** os mecanismos opcionais:

```bash
bash instalar_dependencias.sh --tudo
```

Veja o guia [DEPENDENCIAS.md](DEPENDENCIAS.md) para comandos, configuração do Argos, pares do Apertium e diagnóstico.

## Configurar a OpenRouter

```bash
llm keys set openrouter
llm openrouter refresh
llm openrouter models --free
```

No arquivo local `credenciais_modelos.sh`, preencha `TRADUZIR_OPENROUTER_KEYS` e edite `TRADUZIR_MODELOS_OPENROUTER` conforme `llm models list`. O plugin usa `OPENROUTER_KEY` em cada subprocesso; as chaves dos provedores permanecem separadas. A OpenRouter não precisa de `extra-openai-models.yaml`.

A configuração pública contém **somente marcadores de exemplo**; nenhum segredo deve ser publicado. O arquivo local `credenciais_modelos.sh` está no `.gitignore`, e `credenciais_modelos.sh.example` é a versão compartilhável sem comentários `#`. O ZIP inclui também uma cópia inicial limpa de `credenciais_modelos.sh`, mas **não envie sua cópia pessoal preenchida ao GitHub**.

## Uso

```bash
printf 'Hello world\n' | traduzir
man bash | traduzir
ls --help 2>&1 | traduzir
```

O menu permite selecionar o mecanismo de tradução e, no caso de API, escolher um modelo ou alternar entre todos. Sem terminal interativo, configure `TRADUZIR_MODO_SEM_TTY=api` no arquivo local.

## Configuração e cuidados

- `TRADUZIR_MAX_TENTATIVAS=3` é o padrão do exemplo público para economizar cotas gratuitas. Ajuste conforme seu uso.
- O `llm` precisa ter os plugins no **mesmo ambiente** que executa o comando. Quando instalado por `pipx`, utilize `pipx inject llm ...`.
- O Argos requer um **pacote de idioma** adicional; o Apertium requer pares linguísticos instalados. Nenhum dos dois é garantido só pela instalação do motor.
- A disponibilidade dos modelos `:free` muda. Confirme o catálogo antes de configurar IDs.
- Antes de publicar, execute `git status` e `git diff --cached` para conferir se não há credenciais reais ou outros dados pessoais.

## Testes

```bash
bash -n traduzir.bash
bash -n credenciais_modelos.sh.example
bash tests/test_smoke.sh
```

O teste rápido usa um `llm` simulado e **não faz chamadas externas nem consome cota de API**.

## Sobre o desenvolvimento

Projeto desenvolvido e aprimorado com auxílio de IA. O funcionamento de provedores externos e a qualidade da tradução dependem das versões, serviços e modelos disponíveis.

Para autorizar reutilização do código por terceiros, escolha e adicione uma licença ao repositório (não incluída nesta distribuição).
