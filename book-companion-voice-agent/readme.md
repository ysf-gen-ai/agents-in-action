# 🎙️ Book Companion Voice Agent — n8n Workflow

A powerful voice-enabled RAG chatbot built using **n8n**, combining book-specific knowledge retrieval with conversational AI, persistent memory, and full voice-to-voice interaction.

---

## 🌟 Features

- 🎙️ **Voice-to-Voice Interface**: Complete audio interaction using OpenAI Whisper and TTS
- 🤖 **Book-Specific AI**: Powered by OpenAI GPT-4o-mini, strictly focused on "Building LLM from Scratch"
- 💾 **Session Memory**: Remembers conversation history using PostgreSQL with custom session management
- 🔍 **Semantic Search**: Advanced document retrieval through vector embeddings
- 📚 **Document Processing**: Automated PDF ingestion and vectorization pipeline
- 🎯 **Real-time Voice**: Webhook-based voice interface for instant audio responses

---

## 🏗️ Architecture

This workflow has two main pipelines:

### 1. Document Processing (Setup - Run Once)

Manual Trigger → Google Drive Download → Text Splitter → Document Loader → Embeddings → Vector Store

### 2. Voice Chat Interface (Runtime - Always Active)

Voice Input → Transcription → RAG Agent → [Memory + LLM + Vector Search] → Text-to-Speech → Voice Response

---

## 🚀 Quick Start

### ✅ Prerequisites

- An `n8n` instance (cloud or self-hosted)
- OpenAI API Key with GPT-4o-mini access
- PostgreSQL database (for conversation memory)
- Supabase account (for vector storage)
- Google Drive API access

---

### 🔑 Required Credentials in n8n

| Service      | Purpose                           |
| ------------ | --------------------------------- |
| OpenAI       | Chat model + embeddings + TTS/STT |
| PostgreSQL   | Stores session-based chat memory  |
| Supabase     | Hosts vector embeddings           |
| Google Drive | Downloads source PDF              |

---

## 📋 Setup Instructions

### Step 1: Document Processing (Run Once)

1. Upload "Building LLM from Scratch" PDF to Google Drive
2. Update the file name in the `Download File` node to match your uploaded PDF
3. Trigger the manual workflow to process and vectorize the book
4. Check Supabase to confirm vector storage completion

### Step 2: Voice Interface (Always Running)

1. Activate the webhook trigger
2. Copy the webhook URL for your voice frontend
3. Send audio files via POST with `x-session-id` headers
4. Receive intelligent voice responses grounded in the book content

---

## 🔧 Configuration

### Document Settings

- Text Splitter: Recursive character splitter for optimal chunking
- Embedding Model: `text-embedding-3-large` for high-quality vectors
- Vector Store Table: `documents` (Supabase)

### Agent Settings

- System Message: Book-specific companion focused on "Building LLM from Scratch"
- Model: `gpt-4o-mini` for cost-effective intelligence
- Tools: `building_llm_from_scratch_tool` (vector search tool)
- Response Format: Maximum 1-2 sentences, direct answers

### Voice Configuration

- Transcription: OpenAI Whisper for audio-to-text
- Voice Generation: OpenAI TTS with "Fable" voice
- Session Management: Custom session keys via headers

### Memory Configuration

- Type: PostgreSQL session-based memory
- Context Window: 20 messages per session
- Persistence: Maintains conversation flow across interactions

---

## 🛠️ Customization

### Update Book Content

- Upload new PDF to Drive → Update file name in Download File node → Run processing pipeline

### Modify Voice Behavior

- Edit system message for different conversation styles
- Change TTS voice (alloy, echo, fable, onyx, nova, shimmer)
- Adjust response length and citation requirements

### Extend Functionality

- Add multiple book support
- Implement different document types (DOCX, web content)
- Add authentication and user management
- Integrate with external APIs

---

## 📊 Example Voice Interactions

**User:** _"What are the key components of an LLM?"_
**Agent:** _"According to the book, LLMs consist of three main components: the tokenizer for text processing, the transformer architecture for learning patterns, and the attention mechanism for understanding relationships."_

**User:** _"How do I implement attention?"_
**Agent:** _"The book explains attention as a mechanism that allows the model to focus on different parts of the input sequence, implemented through query, key, and value matrices."_

**User:** _"What about training costs?"_
**Agent:** _"The book discusses training costs in relation to compute requirements, data preparation, and infrastructure considerations for LLM development."_

---

## 🧪 Troubleshooting

### 🛑 No Voice Response?

- Ensure webhook URL is correct and accessible
- Verify audio format compatibility
- Check OpenAI API key permissions for TTS/STT

### 📚 Document Not Found?

- Confirm vectors are stored in Supabase
- Validate embeddings format and table structure
- Check Google Drive file permissions

### ❌ Memory Issues?

- Verify PostgreSQL connection and credentials
- Check session ID headers in requests
- Ensure database tables are created properly

### 🎙️ Audio Quality Issues?

- Use supported audio formats (MP3, WAV, M4A)
- Ensure clear audio input for better transcription
- Check microphone permissions and quality

---

## 📈 Optimization

### 💸 Cost Management

- Use GPT-4o-mini for cost-effective responses
- Optimize chunk size and retrieval count
- Implement response caching for frequent queries

### ⚡ Performance

- Tune similarity thresholds for better retrieval
- Use indexed vector search in Supabase
- Implement async processing for large documents

### 🎯 Accuracy

- Fine-tune system prompts for book-specific responses
- Adjust context window size for better memory
- Optimize embedding model for domain-specific content

---

## 🔐 Security

- Store all credentials securely in n8n credential store
- Use read-only database access where possible
- Implement webhook authentication for production
- Define data retention policies for conversation history
- Secure session management with proper ID generation

---

## 📚 Resources

- 📖 [n8n Documentation](https://docs.n8n.io/)
- 🧠 [LangChain Node Integration](https://docs.n8n.io/integrations/langchain/)
- 🎙️ [OpenAI Audio API](https://platform.openai.com/docs/guides/speech-to-text)
- 🗄️ [Supabase Vector Guide](https://supabase.com/docs/guides/ai)

---

## 🤝 Contributing

We welcome contributions:

- 🐛 Bug reports and fixes
- 🚀 Feature enhancements
- 📝 Documentation improvements
- 🔧 Performance optimizations

---

## 📄 License

Provided for educational and practical use. Please comply with the terms of service of all APIs and services used.

---

## 🙏 Acknowledgments

Built for book companions and voice-enabled AI learning experiences. Special thanks to the n8n and LangChain communities for their powerful integration capabilities.
