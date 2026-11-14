# 🎙️ Entrevistador por Voz Multilíngue

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jcalmeida-ds/entrevistador-por-voz-multilingue/blob/main/entrevistador_por_voz.ipynb)

Simulador de entrevista de emprego por voz, em vários idiomas. Você responde falando, o sistema transcreve com **Whisper**, um entrevistador baseado no **ChatGPT** responde no mesmo idioma e a resposta é falada com **gTTS**. No final, o sistema gera um feedback estruturado da sua performance.

## Demonstração

![Transcrição e resposta do entrevistador](imagens/conversa.png)
![Feedback final](imagens/feedback.png)

## Como funciona

```
Microfone → Whisper (STT) → texto + idioma detectado
          → ChatGPT (entrevistador) → gTTS (TTS) → áudio da pergunta
                      ↓
            histórico da conversa → feedback final
```

## Funcionalidades

- **Conversa por voz multilíngue:** o idioma é detectado pelo Whisper e o entrevistador responde no mesmo idioma
- **Três modos de entrevista**, trocando apenas o prompt de sistema:
  - `fit_cultural`: colaboração, aprendizado, ownership, lidar com erros e feedback
  - `tecnica_ia`: engenharia de prompt, avaliação de LLMs, APIs e Python
  - `ingles`: entrevista conduzida em inglês
- **Método STAR:** quando a resposta é vaga, o entrevistador pede um exemplo concreto (situação, tarefa, ação, resultado)
- **Feedback final estruturado:** nota, pontos fortes, pontos a melhorar, avaliação do STAR, resposta reescrita e perguntas para treinar
- **Sessões salvas em JSON** para comparar a evolução

## Engenharia de prompt

O comportamento do entrevistador vem dos prompts de sistema da seção 4 do notebook. Decisões de design:

- frases curtas e sem markdown, porque o texto será falado
- uma pergunta por vez
- idioma de resposta igual ao do candidato
- feedback só ao final, com temperatura baixa para maior consistência

## Teste multilíngue

| Idioma | Pergunta de teste | Idioma detectado | Resposta no mesmo idioma? |
|---|---|---|---|
| Português | "Fale sobre você." | | |
| English | "Tell me about yourself." | | |
| Español | "Cuéntame sobre ti." | | |

## Como rodar

1. Clique no botão **Open in Colab** acima
2. Gere uma chave em [platform.openai.com](https://platform.openai.com) e adicione-a nos **Secrets** do Colab (ícone de chave) com o nome `OPENAI_API_KEY`, ativando o acesso ao notebook
3. Execute as células em ordem e permita o acesso ao microfone quando o navegador pedir

> A chave nunca deve ser escrita no código. O uso da API da OpenAI é pago por uso.

## Tecnologias

Python · OpenAI API (Whisper e Chat Completions) · gTTS · Google Colab

## Limitações e próximos passos

- **Latência:** cada turno passa por três serviços em sequência
- **Custo:** Whisper e Chat são cobrados por uso
- **Voz do gTTS:** sintética, sem controle de emoção
- **Gravação com tempo fixo:** sem detecção automática do fim da fala
- **Próximos passos:** interface com Gradio, métricas de fala (tempo e palavras de preenchimento), banco de perguntas por vaga e avaliação automática com rubrica

## Autor

**José Carlos Almeida**
[LinkedIn](https://www.linkedin.com/in/jcalmeida-datascience) · [GitHub](https://github.com/jcalmeida-ds)
