# traduzir

**Tradutor de saídas do terminal GNU/Linux**, desenvolvido com auxílio de inteligência artificial (IA).

O projeto permite traduzir textos de comandos e manuais para português usando o pipe (`|`), procurando primeiro uma tradução nativa do sistema, quando disponível. Caso não exista, oferece tradução por APIs de IA, `translate-shell`, Apertium e Argos Translate.

Ele também inclui um bloqueador opcional para preservar comandos, parâmetros, caminhos e outras partes técnicas que não devem ser traduzidas, além de cache e organização das traduções salvas.

## Uso

```bash
man sway | traduzir
ls --help | traduzir
```

Após a execução, escolha o tradutor no menu, se nenhuma tradução nativa tiver sido encontrada.

## Instalação

1. Copie `traduzir.bash` e `credenciais_modelos.sh` para `~/.config/traduzir/`.
2. Configure suas chaves e modelos em `credenciais_modelos.sh`, caso queira utilizar APIs de IA.
3. Adicione ao `~/.bashrc`:

   ```bash
   source "$HOME/.config/traduzir/traduzir.bash"
   ```

4. Recarregue o terminal com `source ~/.bashrc`.

O projeto requer Bash e Python 3. Cada mecanismo de tradução exige suas próprias dependências. Os comandos sugeridos para instalar `translate-shell`, Apertium e Argos estão comentados em `credenciais_modelos.sh`.

**Observação:** o Apertium pode não dispor de um par direto inglês → português. A tradução via espanhol só é utilizada mediante escolha explícita.

## Desenvolvimento

Este projeto foi **criado e aprimorado com o auxílio de IA**, incluindo a implementação e a revisão de código. As traduções e a compatibilidade dos mecanismos dependem das ferramentas e dos modelos instalados.
