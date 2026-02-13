# 🧠 ML Voice Assistant – V1

**Assistente de voz pessoal desenvolvido em Python com pipeline completo de IA:**

**captura de áudio → transcrição → processamento com LLM → resposta por síntese de voz**

---

## 📋 Índice
- [Sobre o Projeto](#-sobre-o-projeto)
- [Pipeline do Sistema](#-pipeline-do-sistema)
- [Tecnologias](#-tecnologias)
- [Pré-requisitos](#-pré-requisitos)
- [Instalação](#-instalação)
- [Como Executar](#-como-executar)
- [Estrutura do Projeto](#-estrutura-do-projeto)
- [Exemplo de Uso](#-exemplo-de-uso)
- [Limitações Atuais](#-limitações-atuais-v1)
- [Roadmap](#-próximas-melhorias-roadmap)
- [Desafios Técnicos](#-desafios-técnicos-enfrentados)
- [Autor](#-autor)

---

## 🎯 Sobre o Projeto

Este assistente de voz é capaz de:
- 🎤 **Ouvir** comandos do usuário via microfone
- 📝 **Transcrever** áudio para texto com Whisper
- 🧠 **Processar** o conteúdo com Google Gemini API
- 🔊 **Responder** verbalmente através de síntese de voz

> ⚠️ **Status:** Versão 1 – Uso pessoal e aprendizado

---

## 🔄 Pipeline do Sistema

```
🎤 Entrada de Áudio
    ↓
📝 Speech-to-Text (Whisper)
    ↓
🧠 Processamento (Gemini API)
    ↓
🔊 Text-to-Speech (pyttsx3)
    ↓
🗣️ Resposta em Áudio
```

---

## 🛠️ Tecnologias

| Categoria | Tecnologia | Função |
|-----------|------------|--------|
| **Linguagem** | Python 3.11+ | Base do projeto |
| **STT** | Whisper (OpenAI) | Transcrição áudio → texto (modelo 'tiny') |
| **LLM** | Google Gemini API | Processamento de linguagem natural |
| **Áudio** | PyAudio + Wave | Captura e manipulação de áudio |
| **TTS** | pyttsx3 | Síntese de voz offline |
| **Concorrência** | Threading | Controle da gravação |

---

## ⚙️ Pré-requisitos

### Dependências de Sistema
- **FFmpeg** (necessário para Whisper)
- **PortAudio** (para PyAudio)

### Dependências Python
```bash
pyaudio
wave
whisper
google-generativeai
pyttsx3
```

---

## 📦 Instalação

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/ml-voice-assistant.git

# Entre no diretório
cd ml-voice-assistant

# Instale as dependências
pip install -r requirements.txt
```

### 🔑 Configuração da API Key

1. Acesse [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Gere sua chave da API Gemini
3. Adicione no código:

```python
genai.configure(api_key="sua_chave_aqui")
```

---

## 🚀 Como Executar

Execute as células do notebook sequencialmente:

| Etapa | Ação |
|-------|------|
| **1** | Pressione ENTER para começar a gravar |
| **2** | Fale seu comando |
| **3** | Pressione ENTER para parar a gravação |
| **4** | Aguarde o processamento automático |
| **5** | Ouça a resposta do assistente |

---

## 📊 Estrutura do Projeto

O notebook `ML-VA.ipynb` contém 4 células principais:

```python
# 1. GRAVAÇÃO
- Captura áudio do microfone
- Salva como 'gravacao.wav'

# 2. SPEECH-TO-TEXT
- Carrega modelo Whisper 'tiny'
- Transcreve áudio para texto
- Salva transcrição em 'transcricao.txt'

# 3. LLM (GEMINI)
- Lê arquivo de transcrição
- Envia para API Gemini
- Retorna resposta processada

# 4. TEXT-TO-SPEECH
- Converte resposta em áudio
- Reproduz via auto-falante
```

---

## 💡 Exemplo de Uso

**Usuário:** "Quais são as linguagens de programação mais utilizadas no mercado atualmente?"

**Processamento:**
```python
# Whisper transcreve o áudio
texto_usuario = "quais são as linguagens de programação mais utilizadas no mercado atualmente"

# Gemini processa e responde
resposta_ia = "Python, JavaScript, Java e C# estão entre as mais utilizadas..."

# pyttsx3 reproduz em voz
engine.say(resposta_ia)
```

**Assistente:** *(responde em áudio com as informações)*

---

## ⚠️ Limitações Atuais (V1)

| Limitação | Descrição |
|-----------|-----------|
| ❌ **Execução única** | Não opera em loop contínuo |
| ❌ **Sem wake word** | Precisa de interação manual |
| ❌ **Dependência de internet** | API Gemini requer conexão |
| ❌ **Processamento síncrono** | Bloqueante durante execução |
| ❌ **Sem tratamento de erros** | Falhas não são capturadas |

---

## 🔮 Próximas Melhorias (Roadmap)

### 🟢 V2 – Melhorias Imediatas
- [ ] Loop contínuo de execução
- [ ] Tratamento de exceções
- [ ] Sistema de logs
- [ ] Configurações externalizadas

### 🟡 V3 – Funcionalidades Avançadas
- [ ] Wake word detection ("Hey Assistente")
- [ ] Comandos específicos (abrir programas, clima)
- [ ] Fallback para modelo local (offline)
- [ ] Suporte a múltiplos idiomas

### 🔴 V4 – Arquitetura Profissional
- [ ] Containerização com Docker
- [ ] API REST com FastAPI
- [ ] Interface web em tempo real
- [ ] Banco de dados para histórico

---

## 🧪 Desafios Técnicos Enfrentados

### 1. **Concorrência na Gravação**
```python
# Solução: Thread paralela para capturar ENTER durante gravação
threading.Thread(target=wait_stop).start()
```

### 2. **Preparação do Texto para TTS**
```python
# Limpeza de caracteres especiais com regex
au = re.sub(r'[^a-zA-Z0-9]', '', resp)
```

### 3. **Performance do Whisper**
- Escolha do modelo 'tiny' (mais leve) para execução local rápida
- Taxa de amostragem configurada para 16000 Hz (otimizada para fala)

### 4. **Integração Jupyter**
- Adaptação do fluxo para execução em células
- Controle manual via `input()` para gravação

---

## 👨‍💻 Autor

**Davi Bezerra Fraga**  
Estudante de desenvolvimento backend e Inteligência Artificial

- 🔗 [LinkedIn](https://www.linkedin.com/in/davi-bezerra-fraga-319a49363/)
- 🐙 [GitHub](https://github.com/Davibzf)
- 📧 [Email](mailto:davibezerrafraga@gmail.com)

---

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

> ⭐ **Se este projeto te ajudou de alguma forma, considere dar uma estrela no GitHub!**  
> 💬 *Feedback e contribuições são sempre bem-vindos*

---

## 📌 Notas Técnicas Importantes

```python
# Configurações utilizadas
RATE = 16000  # Hz (otimizado para reconhecimento de fala)
CHUNK = 10000  # Tamanho do buffer
FORMAT = pyaudio.paInt16  # Formato de áudio
CHANNELS = 1  # Mono (ideal para voz)
```

**Observações:**
- O modelo Whisper 'tiny' foi escolhido por equilíbrio entre precisão e performance local
- pyttsx3 opera totalmente offline, sem dependência de nuvem
- Taxa de 16000 Hz é padrão para sistemas de reconhecimento de fala
