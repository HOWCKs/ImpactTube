# ImpactTube — mapeamento técnico para o redesign

## Diagnóstico do código aberto

A base importada do NewPipe separa as responsabilidades principais e permite uma migração incremental:

- `app/src/main/java/org/schabi/newpipe/MainActivity.java`: shell Android, drawer e navegação atual.
- `app/src/main/java/org/schabi/newpipe/fragments`: listas, detalhes, busca, histórico e inscrições.
- `app/src/main/java/org/schabi/newpipe/player`: player, fila, reprodução em segundo plano e mini player.
- `app/src/main/java/org/schabi/newpipe/download`: diálogo, atividade e integração do fluxo de download.
- `app/src/main/java/org/schabi/newpipe/database`: Room, histórico, playlists, inscrições e estados locais.
- `extractor/`: resolução de fontes, metadados e URLs; não será alterado pelo redesign.
- `shared/src/commonMain`: telas Compose Multiplatform novas de configurações/Sobre; será a referência para componentes modernos.

## Nova arquitetura de informação

O shell visual terá cinco destinos: **Dashboard, Novo download, Downloads, Arquivos e Configurações**. O player, fila, fontes e descoberta existentes continuam disponíveis a partir do Dashboard e dos detalhes, evitando regressão funcional.

## Mapeamento de funções

| Função existente | Nova apresentação |
| --- | --- |
| Busca e entrada de URL | campo principal do Dashboard e tela Novo download |
| `DownloadActivity` / `DownloadDialog` | fluxo colar → analisar → opções → iniciar |
| downloads ativos | cards com progresso, velocidade, ETA e ações |
| downloads concluídos | Arquivos por categoria, grade/lista e filtros |
| histórico e playlists | seções secundárias da biblioteca/arquivos |
| player e `PlayQueue` | mini player persistente e detalhe do conteúdo |
| configurações | grupos Perfil, Downloads, Reprodução, Aparência, Dados |
| banco Room | fonte única para estados, histórico e arquivos locais |
| extractor | serviço de metadados intacto |

## Estratégia de implementação

1. Consolidar tokens de tema, superfícies, raios, elevação e estados.
2. Criar componentes reutilizáveis para card de download, progresso, chip, empty state e bottom sheet.
3. Introduzir o Dashboard sem remover o shell antigo, usando feature flag durante a migração.
4. Migrar o download para o novo fluxo preservando callbacks, permissões e workers.
5. Migrar arquivos e detalhes.
6. Remover apenas telas antigas substituídas depois dos testes de regressão.

## Regras

- Não duplicar lógica de extractor, player ou Room na camada visual.
- Não bloquear a UI durante análise ou download.
- Toda ação deve possuir estado loading, success e erro recuperável.
- O ícone ImpactTube V5 Sunset permanece inalterado.
- A interface deve funcionar com fonte ampliada e modo de animação reduzida.
