# Changelog — IBC-Br por mês

## 1.3.0 — 2026-10-16
### Alterado
- Carga sob demanda no lugar do histórico completo:
  - Ao abrir, baixa só de janeiro de (ano atual − 2) até o último dado: 12 requisições, cerca de 30 pontos por série. A página sempre abre no último mês disponível, e todos os meses do ano dele ficam disponíveis sem nova carga.
  - Ao abrir um mês cuja janela (m−23..m) ainda não foi baixada, baixa os 5 anos ao redor (y−2 a y+2), mais os 2 anos de histórico que eles precisam: 12 requisições de até 7 anos.
- O cache guarda, por série, os valores e os intervalos já baixados. Prefixo `ibcbr:v4:`; os anteriores são limpos na abertura.
- Novas funções puras testadas: `unirIntervalos`, `cobre`, `janelaNecessaria` e `faixaAoRedor`. Saiu `ultimoMesComum`.

## 1.2.0 — 2026-10-16
### Corrigido
- Valores vazios, nulos ou não positivos do SGS não viram mais `0` (antes geravam −100% ou "∞").
- "Recarregar dados" descarta todo o cache, inclusive o último mês disponível, e um mês recém-divulgado aparece na hora.
- Resposta não JSON do SGS (página HTML de erro) mostra "resposta inválida do SGS".
- O modo escuro não pisca mais em claro ao abrir (o tema é aplicado no `<head>`).

### Alterado
- O histórico completo de cada série é baixado uma vez (em blocos de até 10 anos) e cacheado por série. A troca de mês é instantânea, sem rede.
- O cache é limpo na inicialização: entradas vencidas, ilegíveis e de versões antigas (`ibcbr:v1:`, `ibcbr:v2:`).
- Os pesos agora ficam num mapa por ano (`PESOS_POR_ANO`). Anos sem pesos não mostram a linha.
- A versão tem fonte única no `<meta name="version">`.
- Campos com nomes descritivos (`varMes`, `carregTri`, `acum12`…), documentados no cabeçalho.
- Linhas de seção como `<th scope="rowgroup">`.
- Google Fonts removido; Ubuntu é usada só se estiver instalada localmente.
- CSP restringe a rede a `api.bcb.gov.br`.

### Adicionado
- `tests/ibcbr.test.mjs` (Node) testa o bloco de cálculo contra `tests/fixture.json`, gerada da planilha oficial por `tests/gerar_fixture.py`.

## 1.1.0
- Removidos o autoteste e a linha de último dado no status.
