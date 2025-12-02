# quantum-fuzzy-image-segmentation-wildfires

Este repositório armazena os códigos e dados usados na implementação de um **pipeline de segmentação de cicatrizes de incêndios florestais** combinando **lógica fuzzy** e **otimização quântica variacional** (QAOA), aplicado a imagens Sentinel-2 do bioma Cerrado.

O código foi desenvolvido no contexto do Trabalho de Conclusão de Curso:

> **Técnicas de computação quântica e segmentação de imagem fuzzy para análise de incêndios florestais: uma perspectiva da cosmotécnica brasileira**  
> Ilum – Escola de Ciência / CNPEM, 2025.

---

## Introdução

O objetivo deste projeto é investigar se algoritmos de **segmentação fuzzy** otimizados por **computação quântica** podem melhorar o mapeamento de áreas queimadas em comparação com métodos clássicos.  

O pipeline integra alguns blocos principais:

1. **Geoprocessamento** de focos de incêndio (INPE, MapBiomas Fogo etc.) e seleção de janelas espaciais em torno dos eventos.
2. **Processamento espectral** de imagens Sentinel-2 (pré e pós-fogo), com cálculo de índices como **NDVI**, **NBR** e **NBR-SWIR** e suas imagens de diferença.
3. **Segmentação**, comparando:
   - K-Means (clássico);
   - Fuzzy C-Means (FCM);
   - Quantum Fast Fuzzy C-Means (QFFCM) otimizado via **QAOA**,

4. **Geração de mascaras de referência (Ground Truth)** manualemente a partir das imagens dos eventos escolhidos. 
4. **Avaliação da Qualidade de Segmentação**
   - Avaliando por métricas internas (Dunn, Davies–Bouldin, Calinski–Harabasz) e externas (Dice, IoU, Hausdorff).

---

## Estrutura do repositório

A organização geral é a seguinte:

- `geoprocessing/`  
  Scripts e notebooks responsáveis por:
  - obter focos de incêndio e selecionar janelas espaciais de análise;
  - baixar imagens Sentinel-2 pré e pós-fogo;
  - calcular índices espectrais (NDVI, NBR, NBR-SWIR) e gerar imagens de diferença para cada cena;
  - preparar os vetores de características dos pixels para entrada nos métodos de segmentação.

- `Imagens_e_indices/`  
  Conjunto de arquivos com:
  - matrizes/arrays dos índices espectrais e suas diferenças para cada imagem analisada;
  - imagens intermediárias usadas nos testes de segmentação;
  - arquivos compactados (`.npz`, por exemplo) com stacks de índices (`diff_ndvi`, `diff_nbr`, `diff_nbrswir` etc.).

- `requirements.txt`  
  Lista de dependências Python necessárias para executar os notebooks.

- `README.md`  
  Este arquivo de documentação.

> Obs.: Os **notebooks Jupyter** do projeto estão organizados para refletir o fluxo lógico do trabalho, desde a extração das imagens até a geração dos mapas de referência e a comparação entre os métodos de segmentação.

---


## Criadores:
As funções utilizadas para qualquer manipulação de dados dentro desse diretório assim como os métodos propostos foram criadas pelos estudantes: 
  - Daniel Bravin Martins, email: daniel23020@ilum.cnpem.br.  
    Aluno do 6° Semestre do Curso de Bacharel em Ciência e Tecnologia, Ilum - Escola de Ciências.
  
  - Karla Rovedo Pascoalini, email: karla23012@ilum.cnpem.br.  
    Aluna do 6° Semestre do Curso de Bacharel em Ciência e Tecnologia, Ilum - Escola de Ciências.
    

O projeto passou pela orientação dos pesquisadores/doutores:
  - Vinicius Francisco Wasques. Email: vinicius.wasques@ilum.cnpem.br 
    Professor pesquisador da Ilum Escola de Ciências.
  - Felipe Fernandes Fanchini. Email: felipe.fanchini@unesp.br 
    Professor pesquisar da UNESP - Rio Claro.

## Agradecimentos:
Agradecemos pela oportunidade e pelo suporte dos pesquisadores citados acima. Também agradecemos ao INPE, a partir de sua equipe de monitoramento de incêndios do programa queimadas, e a todos aqueles que de alguma forma ajudaram na concepção e construção desse projeto.

---

## Instalação

Recomenda-se usar um ambiente virtual (conda ou `venv`).

```bash
# Clonar o repositório
git clone https://github.com/MrBravin/quantum-fuzzy-image-segmentation-wildfires.git
cd quantum-fuzzy-image-segmentation-wildfires

# Criar ambiente (exemplo com venv)
python -m venv .venv
```bash
# Instalar dependências
pip install -r requirements.txt
