# LangChain Chatbot - Scrimba Knowledge Bank

A modern, interactive chatbot built with LangChain.js that provides intelligent responses about Scrimba's courses and services. This project demonstrates the power of AI-powered conversational interfaces using vector embeddings and retrieval-augmented generation (RAG).

## 🚀 Features

- **Intelligent Q&A**: Powered by OpenAI's GPT models for natural language understanding
- **Vector Search**: Uses Supabase vector store for semantic document retrieval
- **Conversation Memory**: Maintains context across conversation turns
- **Modern UI**: Clean, responsive interface with real-time chat experience
- **RAG Architecture**: Retrieval-Augmented Generation for accurate, contextual responses

## 🛠️ Tech Stack

- **Frontend**: Vanilla JavaScript, HTML5, CSS3
- **Build Tool**: Vite
- **AI/ML**: LangChain.js, OpenAI GPT
- **Vector Database**: Supabase Vector Store
- **Embeddings**: OpenAI Embeddings
- **Styling**: Custom CSS with Google Fonts

## 📋 Prerequisites

Before running this project, you'll need:

- Node.js (v16 or higher)
- npm or yarn
- OpenAI API key
- Supabase account with vector store setup

## 🔧 Installation

1. **Clone the repository**

   ```bash
   git clone <your-repo-url>
   cd langchain-chatbot
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Set up environment variables**

   Create a `.env` file in the root directory with the following variables:

   ```env
   VITE_OPENAI_API_KEY=your_openai_api_key_here
   VITE_SUPABASE_API_KEY=your_supabase_api_key_here
   VITE_SUPABASE_URL_LC_CHATBOT=your_supabase_url_here
   ```

## 🚀 Running the Project

### Development Mode

```bash
npm run dev
# or
npm start
```

### Build for Production

```bash
npm run build
```

### Preview Production Build

```bash
npm run preview
```

The application will be available at `http://localhost:5173` (or the port shown in your terminal).

## 🔑 Environment Variables

| Variable                       | Description                                       | Required |
| ------------------------------ | ------------------------------------------------- | -------- |
| `VITE_OPENAI_API_KEY`          | Your OpenAI API key for GPT models and embeddings | Yes      |
| `VITE_SUPABASE_API_KEY`        | Your Supabase API key for vector store access     | Yes      |
| `VITE_SUPABASE_URL_LC_CHATBOT` | Your Supabase project URL                         | Yes      |

## 🏗️ Project Structure

```
langchain-chatbot/
├── index.html              # Main HTML file
├── index.js               # Main JavaScript application
├── index.css              # Styles
├── package.json           # Dependencies and scripts
├── vite.config.js         # Vite configuration
├── utils/                 # Utility functions
│   ├── retriever.js      # Vector store retriever setup
│   ├── combineDocuments.js # Document combination utility
│   └── formatConvHistory.js # Conversation history formatter
└── images/               # Static assets
    ├── logo-scrimba.svg
    ├── scrimba-bg.jpeg
    └── send.svg
```

## 🧠 How It Works

1. **User Input**: User types a question in the chat interface
2. **Question Processing**: The system converts the question to a standalone question using conversation history
3. **Vector Retrieval**: Relevant documents are retrieved from the Supabase vector store
4. **Context Assembly**: Retrieved documents are combined with conversation history
5. **AI Response**: GPT generates a contextual response based on the assembled information
6. **Display**: The response is displayed in the chat interface

## 🔧 Configuration

### Supabase Vector Store Setup

1. Create a Supabase project
2. Set up a vector store table named `documents` with the following columns:

   - `id` (uuid, primary key)
   - `content` (text)
   - `metadata` (jsonb)
   - `embedding` (vector)

3. Create a function for similarity search:
   ```sql
   CREATE OR REPLACE FUNCTION match_documents(
     query_embedding vector(1536),
     match_count int DEFAULT 5
   )
   RETURNS TABLE (
     id uuid,
     content text,
     metadata jsonb,
     similarity float
   )
   LANGUAGE plpgsql
   AS $$
   BEGIN
     RETURN QUERY
     SELECT
       documents.id,
       documents.content,
       documents.metadata,
       1 - (documents.embedding <=> query_embedding) AS similarity
     FROM documents
     ORDER BY documents.embedding <=> query_embedding
     LIMIT match_count;
   END;
   $$;
   ```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built as part of the [Scrimba LangChain.js course](https://scrimba.com/learn-langchainjs-c02t/~0q)
- Powered by [LangChain.js](https://js.langchain.com/)
- Vector storage provided by [Supabase](https://supabase.com/)
- AI capabilities from [OpenAI](https://openai.com/)

## 📞 Support

If you have any questions or need help, please:

- Open an issue in this repository
- Contact Scrimba support at help@scrimba.com

---

**Happy Coding! 🚀**
