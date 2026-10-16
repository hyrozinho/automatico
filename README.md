# /automatico — Low Ticket Automatizado

Skill pro [Claude Code](https://claude.ai/claude-code) que transforma operacao de low ticket digital num software interativo. Mineracao de ofertas escaladas, modelagem de funil, geracao de criativos, cadastro em gateway e otimizacao de campanhas — tudo dentro do terminal.

**by [@ogestorsantiago_](https://instagram.com/ogestorsantiago_)**

## O que faz

| Modulo | Descricao |
|--------|-----------|
| [1] Setup | Diagnostico de dependencias |
| [2] Minerar | Reclame Aqui, Biblioteca Meta, RatoAds |
| [3] Analisar | Analise completa de oferta + definir produto |
| [4] Entregavel | Gera PDF/pack/planilha/simulado completo |
| [5] Funil | Modela pagina de vendas a partir do concorrente |
| [6] Criativos | Scrapa ads reais, transcreve, gera 7 criativos modelados |
| [7] Gateway | Cadastra produto na Wiapy automaticamente |
| [8] Meta Ads | Cria pixel, campanha e otimiza (metodo @ogestorsantiago_) |
| [9] Config | Diagnostico, instalacao, metricas |

## Instalacao

### Windows (PowerShell)

```powershell
# Baixar o repositorio
git clone https://github.com/guifln2007/automatico.git

# Instalar a skill para sua conta do Claude Code
New-Item -ItemType Directory -Force "$HOME/.claude/skills/automatico" | Out-Null
Copy-Item -Path ".\automatico\*" -Destination "$HOME/.claude/skills/automatico" -Recurse -Force

# Criar a configuracao local do projeto (nao compartilhe esse arquivo)
Copy-Item ".\automatico\config-automatico.example.json" ".\automatico\config-automatico.json"

# Entrar no projeto e iniciar o Claude Code
Set-Location .\automatico
claude
```

### macOS / Linux (Bash)

```bash
git clone https://github.com/guifln2007/automatico.git
mkdir -p "$HOME/.claude/skills/automatico"
cp -R automatico/. "$HOME/.claude/skills/automatico/"
cp automatico/config-automatico.example.json automatico/config-automatico.json
cd automatico
claude
```

No Claude Code, digite `/automatico` e escolha `[1] Setup & Diagnostico`. O arquivo `config-automatico.json` fica no diretorio do projeto em que o Claude Code foi iniciado; preencha nele apenas as credenciais dos servicos que for usar. Ele esta no `.gitignore` e nao deve ser enviado ao GitHub.

Para testar uma alteracao em `SKILL.md` no checkout, atualize a copia instalada antes de abrir o Claude Code:

```powershell
Copy-Item ".\SKILL.md" "$HOME/.claude/skills/automatico/SKILL.md" -Force
```

O Claude Code carrega a skill instalada nesse caminho. Execute o Claude Code a partir da pasta do projeto para que `config-automatico.json` fique nesse projeto.

## Dependencias

Rode `[1] Setup` pra verificar tudo automaticamente. Resumo:

- **Edge** — scraper Reclame Aqui (Windows)
- **Whisper** — transcrever videos (`pip install openai-whisper`)
- **yt-dlp** — baixar videos (`pip install yt-dlp`)
- **Apify** — scraper Biblioteca de Anuncios (conta free em apify.com)
- **Meta Ads Graph API** — criar app em developers.facebook.com, gerar token
- **Wiapy** — gateway de checkout (conta em wiapy.com)
- **RatoAds** — mineracao premium (opcional, ratoads.com.br)

### MCPs opcionais (Claude Code)

- **Higgsfield** — gerar imagens/videos com IA
- **Utmify** — dashboards de performance

## Minerador Reclame Aqui

O `minerador-reclameaqui.py` scrapa reclamacoes de 8 gateways pra encontrar ofertas escaladas.

```bash
# Todos os 8 gateways
python minerador-reclameaqui.py

# Gateways especificos
python minerador-reclameaqui.py wiapy,cakto,kirvano 10 15
```

Requer Edge instalado. Resultados salvos em `./mineracao/`.

## Estrutura de pastas (geradas automaticamente)

```
./mineracao/          resultados do Reclame Aqui
./analises/           analises de ofertas salvas
./produtos/           definicoes de produto
./entregaveis/        PDFs, packs, planilhas gerados
./funis/              paginas de vendas HTML
./criativos/          roteiros, vozes, videos de fundo
```

## Licenca

MIT
