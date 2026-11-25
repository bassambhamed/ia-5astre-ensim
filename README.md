<p align="center">
  <img src="assets/ia-au-llm.png" alt="De l'IA au LLM agentique : du réseau de neurones au LLM, puis à la boucle d'agent" width="100%">
</p>

# De l'IA au LLM agentique

Cours de 5<sup>e</sup> année de l'**ENSIM** (Le Mans Université), parcours **ASTRE** (Architecture des Systèmes Temps Réel et Embarqués) : sept séances de 1 h 15, du **24 au 27 novembre 2026**, pour aller du neurone formel aux agents LLM en gardant en tête la contrainte d'un système embarqué.

![Slides](https://img.shields.io/badge/slides-PDF-1D3960)
![Labs](https://img.shields.io/badge/labs-Jupyter%20%C2%B7%20Colab-D25E3A)
![Langue](https://img.shields.io/badge/langue-fran%C3%A7ais-2a7f7f)

**Intervenants** : Bassem Ben Hamed et Ali Khalfallah.

---

## Sommaire

1. [Présentation](#présentation)
2. [Programme et supports](#programme-et-supports)
3. [Acquis d'apprentissage](#acquis-dapprentissage)
4. [Contenu des séances](#contenu-des-séances)
5. [Résultats mesurés](#résultats-mesurés)
6. [Et sur cible embarquée ?](#et-sur-cible-embarquée-)
7. [Structure du dépôt](#structure-du-dépôt)
8. [Exécuter les labs](#exécuter-les-labs)
9. [Données, modèles et licences](#données-modèles-et-licences)
10. [Limites connues](#limites-connues)
11. [Références](#références)
12. [Auteurs et licence](#auteurs-et-licence)

---

## Présentation

### Public

Élèves ingénieurs de 5<sup>e</sup> année, spécialité Informatique, parcours ASTRE. D'après la fiche RNCP42418, le parcours forme aux « architectures logicielles sous contraintes matérielles et énergétiques ». Le cours s'appuie sur deux blocs de compétences :

- **BC04** : capteurs, traitement du signal et de l'image sur DSP, FPGA ou ARM, sécurité IoT, edge computing ;
- **BC05** : OS temps réel, bare-metal, HAL, microcontrôleurs ARM.

### Pédagogie

- **Les slides se suffisent à elles-mêmes.** Il n'y a pas de démonstration en direct : chaque formule est posée dans un encadré, puis développée pas à pas sur un exemple numérique avec de petites valeurs.
- **Les labs sont faits en autonomie après la séance.** Ils sont envoyés aux étudiants, qui valident chaque séance : recalcul des exemples des slides, expériences sur de vraies données, puis exercices vérifiés automatiquement.
- **Chaque nombre est vérifié.** Les valeurs des exemples numériques sont recalculées en Python avant d'être écrites sur une slide, puis refaites dans la partie A du lab correspondant.
- **Chaque séance a son encadré « Et sur cible embarquée ? »** avec des ordres de grandeur pour un STM32F446 (Cortex-M4 à 180 MHz, 512 Ko de Flash, 128 Ko de SRAM).

### Deux fils rouges

| Fil | Séances | Tâche | Données |
|---|---|---|---|
| **A. Capteur intelligent et maintenance prédictive** | S1 à S3, puis le lab 4b | Classer les pannes d'une machine ; estimer la durée de vie restante (RUL) ; estimer l'usure de l'outil sans capteur (lab 4b) | AI4I 2020 ; NASA C-MAPSS FD001 |
| **B. Assistant vocal pour la maison ou l'usine connectée** | S4 à S7 | Classer l'intention d'une commande en français. **La même tâche est reprise à chaque séance** : GRU, CamemBERT, LLM en zero-shot, puis LLM avec LoRA, RAG et agent | Amazon MASSIVE 1.1 fr-FR, partition officielle ; sous-ensemble `iot_*` pour les LLM |

Un fil conducteur traverse aussi les séances 6 et 7 : la **fonction FreeRTOS fictive `xTaskBoostPriorityFromISR()`**. Elle n'existe pas (le lab 4 vérifie qu'elle est absente du noyau). Un LLM la décrit avec assurance en S6, et le RAG de la S7 répond qu'elle est absente de la documentation.

---

## Programme et supports

| Séance | Créneau | Salle | Thème | Slides | Lab |
|---|---|---|---|---|---|
| **S1** | mar. 24/11 · 9h30–10h45 | TD1 | Panorama : IA, ML, DL, IA générative, cycle de vie, MLOps | [PDF](slides/S1_panorama_ia.pdf) (41 p.) | [Lab 1][c1] |
| **S2** | mer. 25/11 · 8h00–9h15 | P22 | Du neurone au perceptron multicouche | [PDF](slides/S2_neurone_mlp.pdf) (42 p.) | [Lab 2][c2] |
| **S3** | mer. 25/11 · 9h30–10h45 | P22 | Apprendre : rétropropagation, optimiseurs, classification et régression | [PDF](slides/S3_retropropagation.pdf) (34 p.) | [Lab 3][c3] |
| **S4** | mer. 25/11 · 11h00–12h15 | P22 | Séquences et texte : RNN, LSTM, GRU | [PDF](slides/S4_rnn_lstm_gru.pdf) (30 p.) | [Lab 4][c4] · [Lab 4b][c4b] |
| **S5** | jeu. 26/11 · 8h00–9h15 | TD1 | Transformers et attention | [PDF](slides/S5_transformers.pdf) (40 p.) | [Lab 5][c5] |
| **S6** | jeu. 26/11 · 13h45–15h00 | TD1 | LLM : fonctionnement et limites | [PDF](slides/S6_llm.pdf) (40 p.) | [Lab 6][c6] |
| **S7** | ven. 27/11 · 13h45–15h00 | P20 | RAG, fine-tuning, agents et workflows agentiques, synthèse | [PDF](slides/S7_rag_agents.pdf) (44 p.) | [Lab 7a][c7a] · [Lab 7b][c7b] |

[c1]: https://colab.research.google.com/github/bassambhamed/ia-5astre-ensim/blob/main/labs/Lab1_paradigmes.ipynb
[c2]: https://colab.research.google.com/github/bassambhamed/ia-5astre-ensim/blob/main/labs/Lab2_neurone_mlp.ipynb
[c3]: https://colab.research.google.com/github/bassambhamed/ia-5astre-ensim/blob/main/labs/Lab3_retropropagation.ipynb
[c4]: https://colab.research.google.com/github/bassambhamed/ia-5astre-ensim/blob/main/labs/Lab4_rnn_lstm_gru.ipynb
[c4b]: https://colab.research.google.com/github/bassambhamed/ia-5astre-ensim/blob/main/labs/Lab4b_rnn_ai4i.ipynb
[c5]: https://colab.research.google.com/github/bassambhamed/ia-5astre-ensim/blob/main/labs/Lab5_transformers.ipynb
[c6]: https://colab.research.google.com/github/bassambhamed/ia-5astre-ensim/blob/main/labs/Lab6_llm.ipynb
[c7a]: https://colab.research.google.com/github/bassambhamed/ia-5astre-ensim/blob/main/labs/Lab7a_rag_agents.ipynb
[c7b]: https://colab.research.google.com/github/bassambhamed/ia-5astre-ensim/blob/main/labs/Lab7b_lora.ipynb

Les liens « Lab » ouvrent le notebook dans Google Colab (branche `main` du dépôt).

---

## Acquis d'apprentissage

À l'issue des sept séances, l'étudiant sait :

1. **Situer** IA, ML, deep learning et IA générative, puis choisir le paradigme adapté (supervisé, non supervisé, auto-supervisé, par renforcement) pour un problème embarqué ou IoT.
2. **Décrire** le cycle de vie d'un modèle, du cadrage au monitoring, et les briques MLOps, y compris leurs spécificités embarquées (mise à jour OTA, flotte, quantification).
3. **Expliquer** le fonctionnement d'un réseau de neurones : propagation avant, fonctions d'activation, fonctions de perte, rétropropagation par la règle de la chaîne, optimiseurs.
4. **Entraîner et évaluer** un MLP en classification et en régression avec les bonnes métriques, puis estimer son empreinte sur un microcontrôleur.
5. **Expliquer** RNN, LSTM et GRU, puis le mécanisme d'attention et l'architecture Transformer.
6. **Expliquer** le fonctionnement d'un LLM (tokens, fenêtre de contexte, échantillonnage) et ses limites : hallucination, date de coupure, non-traçabilité, sécurité.
7. **Choisir** entre prompt engineering, RAG, fine-tuning (LoRA), workflow agentique et agent autonome, en justifiant le choix pour un système critique.

---

## Contenu des séances

<details>
<summary><b>S1 · Panorama de l'IA</b></summary>

**Objectifs** : définir les termes, distinguer les paradigmes, comprendre qu'un modèle s'inscrit dans un cycle de vie.

1. *Définir l'intelligence artificielle* : IA, machine learning, deep learning et IA générative.
2. *Les paradigmes d'apprentissage* : supervisé, non supervisé, auto-supervisé, par renforcement.
3. *Du notebook à la production* : cycle de vie d'un modèle, MLOps, contraintes de l'embarqué.
4. *Synthèse* : ce qu'il faut retenir.

**Lab 1** (CPU, environ une minute) : AI4I 2020 traité en supervisé (prédire la panne), non supervisé (détecter l'atypique sans étiquettes) et par renforcement (Q-learning pour chauffer une pièce) ; carte de modèle ; dérive d'un capteur et indice PSI.
</details>

<details>
<summary><b>S2 · Du neurone au perceptron multicouche</b></summary>

**Objectifs** : comprendre ce que calcule un neurone, pourquoi il faut des couches cachées et des non-linéarités, et ce que mesure une fonction de perte.

1. *Le neurone et le perceptron* : ce qu'un perceptron apprend, et ce qu'il ne peut pas apprendre (XOR).
2. *Empiler des neurones* : le perceptron multicouche, un calcul qui se ramène à des MAC.
3. *Fonctions d'activation* : la non-linéarité, et ce qu'elle coûte sur un microcontrôleur.
4. *Fonctions de perte* : MSE, entropie croisée.
5. *Vers l'apprentissage* : la descente de gradient, avant la rétropropagation.

**Lab 2** (CPU, moins d'une minute) : perceptron, XOR, MLP, activations, pertes, descente de gradient.
</details>

<details>
<summary><b>S3 · Apprendre : rétropropagation et optimiseurs</b></summary>

**Objectifs** : calculer un gradient à la main, comprendre les optimiseurs, entraîner et évaluer un MLP sur deux cas réels, puis estimer son coût sur une cible embarquée.

1. *La rétropropagation* : le gradient de la perte par rapport à chaque poids, en un seul passage arrière.
2. *Les optimiseurs* : du pas fixe à Adam, et le choix du taux d'apprentissage.
3. *Généraliser* : un modèle n'est bon que sur des données qu'il n'a pas vues.
4. *Deux cas d'usage* : maintenance prédictive (pannes AI4I, durée de vie restante C-MAPSS), puis coût sur un STM32.

**Lab 3** (CPU, environ 2 minutes) : rétropropagation à la main contre autograd, optimiseurs, MLP sur AI4I et C-MAPSS, export ONNX et quantification int8.
</details>

<details>
<summary><b>S4 · Séquences et texte : RNN, LSTM, GRU</b></summary>

**Objectifs** : représenter du texte, comprendre la récurrence et ses limites, distinguer LSTM et GRU, puis choisir une architecture de séquence.

1. *Du texte aux nombres* : tokenisation, one-hot, embeddings.
2. *Les réseaux récurrents* : état caché, rétropropagation dans le temps, gradient qui s'évanouit.
3. *LSTM et GRU* : des portes qui décident quoi garder, écrire et oublier.
4. *Architectures et cas d'usage* : un même bloc récurrent, quatre façons de le brancher.

**Lab 4** : intentions MASSIVE fr-FR avec RNN, LSTM et GRU ; gradient mesuré dans chaque cellule ; LSTM par caractères entraîné sur le noyau FreeRTOS, avec l'effet de la température d'échantillonnage.

**Lab 4b** (CPU, environ 5 minutes), entièrement consacré à AI4I 2020 (fil A) : contexte de la maintenance prédictive et du jeu ; variables expliquées une à une, avec les règles des modes de panne ; analyse exploratoire, structure temporelle, découpage par outil ; détection des pannes comparée à un MLP et à une forêt aléatoire, puis interprétée (longueur de fenêtre, saillance, rappel par mode, importance par permutation) ; enfin, un capteur virtuel qui estime l'usure de l'outil sans capteur, et la cellule du LSTM recalculée à la main.
</details>

<details>
<summary><b>S5 · Transformers</b></summary>

**Objectifs** : comprendre la self-attention et le bloc Transformer, distinguer les trois familles, voir le Transformer appliqué à l'image et à l'audio.

1. *Le mécanisme d'attention* : remplacer la récurrence par un accès direct à toute la séquence.
2. *Trois familles de Transformers* : encodeur (BERT), décodeur (GPT), encodeur-décodeur (T5, Whisper).
3. *Au-delà du texte* : ViT pour l'image, AST et Whisper pour l'audio.
4. *Adapter et embarquer* : fine-tuning d'un modèle pré-entraîné, distillation, quantification.

**Lab 5** : attention recalculée à la main, mini-Transformer entraîné de zéro, fine-tuning de CamemBERT, puis (optionnel) chaîne voix → texte → intention avec Whisper tiny.
</details>

<details>
<summary><b>S6 · LLM : fonctionnement et limites</b></summary>

**Objectifs** : expliquer comment un LLM est construit et génère du texte, maîtriser tokens et fenêtre de contexte, identifier et démontrer ses limites.

1. *Du Transformer au LLM* : entropie croisée, perplexité, lois d'échelle, alignement.
2. *Tokens et contexte* : BPE, fenêtre de contexte, KV-cache.
3. *Générer du texte* : softmax à température, top-k, top-p.
4. *Modèles et cibles embarquées* : mémoire des poids, bande passante, quantification.
5. *Les limites* : hallucination, date de coupure, non-traçabilité, non-déterminisme, biais, prompt injection, coût.

**Lab 6** : Qwen3-1.7B ; tokens et perplexité ; échantillonnage ; hallucination sur la fonction fictive ; date de coupure lue sur l'API GitHub ; injection de prompt ; classification zero-shot de 220 commandes en JSON ; mémoire et KV-cache mesurés.
</details>

<details>
<summary><b>S7 · RAG, fine-tuning, agents et workflows agentiques</b></summary>

**Objectifs** : choisir la bonne technique pour corriger une limite, construire un RAG, comprendre LoRA, distinguer un workflow agentique d'un agent autonome et justifier ce choix pour un système critique.

1. *Corriger les limites d'un LLM* : prompt, RAG, fine-tuning, dans cet ordre.
2. *Le RAG* : découpage, embeddings, recherche dense, lexicale (BM25) et hybride, reclassement, évaluation (recall@k, fidélité).
3. *Fine-tuning et LoRA* : `W' = W + (α/r)·B·A`, initialisation de `B` à zéro, QLoRA.
4. *Agents* : appel d'outils, boucle pensée-action-observation, coût en tokens.
5. *Workflows agentiques et garde-fous* : choisir le bon degré d'autonomie.
6. *Synthèse du cours*.

**Lab 7a** : RAG sur le *FreeRTOS Kernel Book* (e5, FAISS, BM25, reclasseur), question sur la fonction fictive avec et sans RAG, workflow contre agent sur un scénario de maintenance. **Lab 7b** : LoRA de zéro, puis avec `peft`, sur MASSIVE `iot_*`.
</details>

---

## Résultats mesurés

Tous les labs ont été exécutés de bout en bout sur un **MacBook Pro Apple M4 Pro (24 Go)**, avec le GPU Metal (MPS) ou le CPU. Les chiffres ci-dessous sont ceux des notebooks, repris dans les slides.

### Fil rouge B : une même tâche, quatre solutions

Exactitude sur les **220 commandes `iot_*` de la partition `test`** de MASSIVE fr-FR :

| Séance | Solution | Exactitude | Classes à départager | Paramètres entraînés |
|---|---|---|---|---|
| S4, S5 | GRU | 78,3 % | 60 | 0,47 M |
| S5 | CamemBERT-base (fine-tuning) | 88,2 % | 60 | 111 M |
| S6 | Qwen3-1.7B, zero-shot | 83,2 % | 9 | 0 |
| S7 | Qwen3-1.7B + LoRA | **93,2 %** | 9 | 17,4 M |

> **À lire avec précaution** : GRU et CamemBERT choisissent parmi 60 intentions, les LLM parmi 9, ce qui avantage les LLM. Une seule exécution par méthode et 220 commandes : l'incertitude est de l'ordre de 2 points.

### Autres mesures

| Séance | Mesure |
|---|---|
| S4 | Sur les 2 974 phrases du `test` (60 intentions, moyenne de 3 graines) : RNN 72,0 %, LSTM 76,9 %, GRU 77,5 %. Gradient d'un réseau non entraîné sur 50 pas : 2,5·10⁻¹⁵ (RNN), 1,8·10⁻¹¹ (LSTM), 3,5·10⁻⁵ avec un biais de la porte d'oubli fixé à 1. |
| S4 | LSTM par caractères sur FreeRTOS : la part d'identifiants générés qui existent dans le noyau passe de 92,3 % à la température 0,2 à 9,1 % à 1,4. |
| S4, lab 4b | Pannes AI4I, découpage par outil (39 pannes de test), fenêtre de 10 cycles, moyenne de 3 graines : précision moyenne (AP) de 0,65 (RNN), 0,65 (LSTM) et 0,63 (GRU), contre 0,78 pour un MLP sur le seul cycle courant et 0,91 pour la forêt aléatoire. Sans passé (T = 1), le LSTM et le GRU remontent à 0,81 et 0,82 : les pannes AI4I dépendent du cycle courant. |
| S4, lab 4b | Sans capteur d'usure, l'usure est reconstituée sur la vie de chaque outil avec une RMSE de 1,3 min (GRU), 1,7 min (LSTM) et 7,1 min (RNN), contre 64 min sans mémoire et 6,3 min pour un compteur de cycles. Avec l'usure estimée par le GRU, la forêt aléatoire retrouve une AP de 0,91 (0,73 sans usure). |
| S5 | Sur le `test` : GRU 77,5 %, mini-Transformer (1,18 M de paramètres) 77,3 %, CamemBERT 86,7 %. |
| S6 | Qwen3-1.7B en fp16 sur MPS : 25,7 tokens/s en génération. En zero-shot, 0,5 % de JSON invalide. Il décrit `xTaskBoostPriorityFromISR()` sans aucun doute et suit une injection de prompt même avec un prompt défensif. |
| S7, RAG | Sur la question à propos de la fonction fictive, 5 tirages à T = 0,7 : sans RAG, 0 réponse sur 5 admet l'absence ; avec RAG, 2 ; avec RAG et garde-fou déterministe, 5. |
| S7, RAG | recall@3 sur 8 questions : dense 78 %, hybride 56 %, hybride et reclassement 66 %, BM25 25 % (questions en français, livre en anglais : ici, le dense seul gagne). |
| S7, agent | Scénario de maintenance, 10 exécutions à T = 0,7 : 10 réussites avec le même enchaînement d'outils. L'agent consomme 1 120 tokens contre 206 pour le workflow, soit 5,4 fois plus. |
| S7, LoRA | Prompt de 53 tokens au lieu de 200. Adaptateur de rang 16 : 17,4 M de paramètres (0,85 % du modèle), 70 Mo en float32. Entraînement : 487 s sur le Mac M4 Pro. |

---

## Et sur cible embarquée ?

Chaque séance se termine par des ordres de grandeur pour le **STM32F446** (Cortex-M4 à 180 MHz, 512 Ko de Flash, 128 Ko de SRAM). Quelques exemples calculés dans les slides et recalculés dans les labs :

| Modèle | Ordre de grandeur |
|---|---|
| MLP 7 → 64 → 32 → 1 (S3) | 2 625 paramètres, 2 528 MAC ; 10,5 ko en float32 (2,0 % de la Flash), 2,6 ko en int8. |
| LSTM d = 16, h = 32, fenêtre de 30 pas (S4) | 6 400 paramètres, 6,4 ko en int8 ; 184 320 MAC ; 2,0 à 4,1 ms à 2 à 4 cycles par MAC (estimation, à mesurer sur cible). |
| GRU d = 11, h = 32, détecteur de pannes AI4I (lab 4b) | 4 353 paramètres, 4,4 ko en int8 ; en flux, 4 160 MAC par nouveau cycle, soit 46 à 92 µs ; état de 128 octets. La forêt aléatoire de référence pèse 3,4 Mo. |
| Mini-Transformer, GRU, CamemBERT (S5) | En int8, le mini-Transformer pèse 1,18 Mo (2,3 fois la Flash) ; CamemBERT 110,7 Mo ; Whisper tiny 39 Mo. Aucun ne tient. |
| Qwen3-1.7B en int4 (S6) | 0,86 Go de poids, plus 0,94 Go de KV-cache à 8 192 tokens. Borne théorique d'un Raspberry Pi 5 : 19,8 tokens/s. Ne tient pas sur un microcontrôleur. |
| Adaptateur LoRA de rang 8 sur q, k, v, o (S7) | 3 211 264 paramètres, 6,4 Mo en bf16, contre 3,4 Go pour le modèle : 536 fois moins à envoyer pour une mise à jour OTA. |

Outils cités dans le cours : ST Edge AI (STM32Cube.AI), LiteRT (ex-TensorFlow Lite Micro), ExecuTorch, Edge Impulse, ONNX Runtime, llama.cpp et GGUF.

---

## Structure du dépôt

```text
ia-5astre-ensim/
├── README.md
├── assets/
│   └── ia-au-llm.png               # bandeau du cours
├── slides/                         # PDF des 7 séances
│   ├── S1_panorama_ia.pdf
│   ├── S2_neurone_mlp.pdf
│   ├── S3_retropropagation.pdf
│   ├── S4_rnn_lstm_gru.pdf
│   ├── S5_transformers.pdf
│   ├── S6_llm.pdf
│   └── S7_rag_agents.pdf
└── labs/                           # notebooks Jupyter, exécutés
    ├── Lab1_paradigmes.ipynb
    ├── Lab2_neurone_mlp.ipynb
    ├── Lab3_retropropagation.ipynb
    ├── Lab4_rnn_lstm_gru.ipynb
    ├── Lab4b_rnn_ai4i.ipynb
    ├── Lab5_transformers.ipynb
    ├── Lab6_llm.ipynb
    ├── Lab7a_rag_agents.ipynb
    └── Lab7b_lora.ipynb
```

---

## Exécuter les labs

### Sur Google Colab

Cliquez sur le lien « Lab » du [tableau du programme](#programme-et-supports). Un GPU T4 est recommandé pour les labs 4 à 7 (*Exécution → Modifier le type d'exécution*), sauf pour le lab 4b, qui tourne sur CPU. Le code choisit seul le périphérique, dans l'ordre CUDA, MPS, CPU, et réduit la taille de l'expérience sur CPU. Un paquet absent s'installe automatiquement avec `%pip install -q`.

### En local

```bash
pip install torch transformers sentence-transformers scikit-learn pandas matplotlib \
            tiktoken datasets rank_bm25 faiss-cpu peft accelerate onnx onnxruntime onnxscript ucimlrepo
jupyter lab labs/
```

Versions utilisées : PyTorch 2.10, Transformers 5.3, PEFT 0.22.

### Structure commune des labs

1. objectifs, prérequis et plan ;
2. rappel des formules ;
3. **partie A** : recalcul des exemples numériques des slides ;
4. **partie B** : expériences sur les données des fils rouges ;
5. **partie C**, « Exercices de validation » : chaque fonction à compléter renvoie `None`, et le vérificateur `verifier(nom, valeur, attendu, tol)` affiche « À compléter », « Correct » ou « Incorrect » ;
6. corrigé, qui redéfinit les fonctions puis relance toute la vérification.

Le lab 4b, entièrement consacré à AI4I, n'a pas de partie A : les exemples de la séance 4 sont recalculés dans le lab 4.

Les notebooks s'exécutent de bout en bout sans erreur, même sans avoir complété les exercices. Chacun télécharge ses données et prévoit un repli si la source est indisponible.

### Durées mesurées (Mac M4 Pro)

| Lab | Durée | Remarque |
|---|---|---|
| 1 · 2 · 3 | de moins d'une minute à environ 2 minutes | CPU suffisant |
| 4 | 6 min 30 s | |
| 4b | 5 min | sur CPU : pour ces réseaux de quelques milliers de paramètres, le GPU MPS est plus lent |
| 5 | 29 min | dont 22 min pour CamemBERT, avec une époque anormalement lente (environ 13 min sinon) |
| 6 | 2 min | modèle déjà téléchargé (4 Go) |
| 7a | 3 min 30 s | modèles déjà téléchargés |
| 7b | 12 min | dont 8 min d'entraînement ; Qwen3-1.7B en float32 avec *gradient checkpointing* |

---

## Données, modèles et licences

| Usage | Ressource | Licence |
|---|---|---|
| S1, S3, lab 4b : pannes et usure | [AI4I 2020 Predictive Maintenance](https://archive.ics.uci.edu/dataset/601) (Matzka, 2020), UCI id 601, jeu synthétique | CC BY 4.0 |
| S3 : durée de vie restante | NASA C-MAPSS FD001 (Saxena et Goebel, 2008), *NASA Prognostics Data Repository* | Données publiques de la NASA |
| S4 à S7 : intentions et slots | Amazon MASSIVE 1.1, fr-FR (FitzGerald et al., 2022), partition officielle `train` / `dev` / `test` ; sous-ensemble `iot_*` (9 intentions, 220 commandes de test) en S6 et S7 | CC BY 4.0 |
| S4 : génération de C | Sources du noyau FreeRTOS (`FreeRTOS-Kernel`) | MIT |
| S5 : encodeur français | [`almanach/camembert-base`](https://huggingface.co/almanach/camembert-base) | MIT |
| S5 : voix | `openai/whisper-tiny` ; synthèse `facebook/mms-tts-fra` pour la phrase d'exemple | Apache 2.0 ; CC BY-NC 4.0 (usage non commercial) pour MMS-TTS |
| S6, S7 : LLM | [`Qwen/Qwen3-1.7B`](https://huggingface.co/Qwen/Qwen3-1.7B) (2,03 G de paramètres, 4,06 Go en fp16), mode sans raisonnement | Apache 2.0 |
| S7 : RAG | *FreeRTOS Kernel Book* (dépôt `FreeRTOS/FreeRTOS-Kernel-Book`, 13 chapitres, 876 extraits de 256 tokens) ; `intfloat/multilingual-e5-small` ; FAISS ; `rank_bm25` ; reclasseur `cross-encoder/ms-marco-MiniLM-L-6-v2` | CC BY-SA 4.0 (livre) ; MIT (e5) ; Apache 2.0 (reclasseur) |
| S7 : LoRA | `peft` 0.22, rang 16 sur les 7 matrices de chaque couche | Apache 2.0 |

Les données et les modèles sont téléchargés par les labs et ne sont pas redistribués dans ce dépôt. Chaque lab rappelle la licence de ce qu'il utilise.

---

## Limites connues

- Les labs ont été exécutés sur un Mac M4 Pro uniquement. **Aucun n'a été exécuté sur un GPU T4 de Colab** : les durées et la mémoire (notamment Qwen3-1.7B en float32 pour LoRA, avec *gradient checkpointing* pour tenir en 16 Go) y restent à mesurer.
- Lab 4b : le test ne contient que 39 pannes (18 outils) ; une panne de plus ou de moins change le rappel de 2,6 points. La description officielle d'AI4I ne correspond pas exactement aux données (proportions des types L, M, H ; nombres de TWF et de RNF) : le lab s'appuie sur les données.
- Les latences sur STM32F446 sont des **estimations** (2 à 4 cycles par MAC), pas des mesures sur cible.
- Les comparaisons du fil rouge B portent sur 220 commandes et une exécution par méthode ; GRU et CamemBERT classent parmi 60 intentions, les LLM parmi 9.
- Les durées du lab 5 varient avec la charge de la machine : le fine-tuning de CamemBERT a pris 571 s lors d'une exécution et 1 296 s lors de la suivante. Les slides donnent la dernière mesure.
- Sur macOS, `faiss` et `torch` embarquent chacun une copie d'OpenMP : le lab 7a pose `KMP_DUPLICATE_LIB_OK` et `faiss.omp_set_num_threads(1)` pour éviter un plantage.
- Dans le lab 5, la transcription de Whisper tiny sur la phrase synthétisée est imparfaite (« Alim, la lumière du salon. » pour « Allume la lumière du salon. »). Les schémas de la S5 montrent l'intention attendue `iot_hue_lighton` ; sur cette phrase, le CamemBERT fine-tuné du lab prédit en réalité `iot_hue_lightup` (probabilité 0,29), une confusion déjà fréquente sur le jeu de test.

---

## Références

- Rosenblatt (1958), *The Perceptron* ; Minsky et Papert (1969), *Perceptrons* ; Rumelhart, Hinton et Williams (1986), *Learning representations by back-propagating errors*.
- Glorot et Bengio (2010) ; He et al. (2015) ; Kingma et Ba (2014), *Adam* ; Loshchilov et Hutter (2019), *AdamW* ; Srivastava et al. (2014), *Dropout* ; Ioffe et Szegedy (2015), *Batch Normalization*.
- Hochreiter et Schmidhuber (1997), *LSTM* ; Cho et al. (2014), *GRU* ; Bahdanau et al. (2014), *attention* ; Du et al. (2017), *DeepLog*.
- Vaswani et al. (2017), *Attention Is All You Need* ; Devlin et al. (2018), *BERT* ; Dosovitskiy et al. (2020), *ViT* ; Gong et al. (2021), *AST* ; Radford et al. (2022), *Whisper*.
- Kaplan et al. (2020) ; Hoffmann et al. (2022) ; Ouyang et al. (2022), *InstructGPT* ; Rafailov et al. (2023), *DPO* ; Liu et al. (2023), *Lost in the Middle*.
- Lewis et al. (2020), *RAG* ; Hu et al. (2021), *LoRA* ; Dettmers et al. (2023), *QLoRA* ; Anthropic (2024), *Building effective agents*.
- Sculley et al. (2015), *Hidden Technical Debt in Machine Learning Systems*.
- Jeux de données : Matzka (2020), AI4I ; Saxena et al. (2008), C-MAPSS ; FitzGerald et al. (2022), MASSIVE.
- Fiche RNCP42418 (France Compétences) ; règlement (UE) 2024/1689 (AI Act) et Omnibus numérique IA (2026).

---

## Auteurs et licence

**Bassem Ben Hamed** et **Ali Khalfallah**, ENSIM, Le Mans Université.

**Licence** : à préciser par les auteurs. En l'absence de licence, les supports de ce dépôt restent la propriété de leurs auteurs. Les jeux de données et les modèles tiers conservent leur propre licence (voir le [tableau ci-dessus](#données-modèles-et-licences)).

Dépôt : <https://github.com/bassambhamed/ia-5astre-ensim>
