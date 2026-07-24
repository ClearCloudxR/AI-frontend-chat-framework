# GPT-5.4 Mini · AI Chat Interface

A lightweight, single-page AI chat interface with Markdown rendering, code highlighting, and file upload support. Designed for the RSC community.

---

## ✨ Features

- Clean, modern chat UI with dark theme
- Markdown rendering with syntax highlighting
- LaTeX formula support via KaTeX
- File upload support (images, text, Office documents)
- Adjustable model parameters (Temperature, Top P, etc.)
- Chat history saved locally
- Export conversation as text, Markdown, or image
- Mobile-friendly responsive design

---

## 🚀 Live Demo

[https://factorization.top/chat](https://factorization.top/chat)

---

## 🛠️ How to Use

### 1. Run Locally

Simply open `chat.html` in your browser. No build tools required.

### 2. Online

Visit the live demo link above.

> ⚠️ **Note**: The interface will display, but **chat functionality requires a backend API proxy**. See the API Configuration section below.

---

## 🔧 API Configuration

This frontend expects a backend API proxy at `https://ai.factorization.top` (or you can modify the `API_URL` variable in the JavaScript).

### How the API works

The chat interface sends requests to:

```
POST https://ai.factorization.top
```

with the following payload:

```json
{
  "model": "deepseek-chat",
  "messages": [...],
  "temperature": 0.2,
  "top_p": 0.85,
  "max_tokens": 2048,
  "stream": true
}
```

The backend proxy should forward requests to your preferred AI provider (DeepSeek, OpenAI, etc.) and return responses in the same format.

### Deploy Your Own Proxy

You can deploy a simple Cloudflare Worker or Vercel Serverless Function to act as a proxy. Example (Cloudflare Worker):

```javascript
export default {
  async fetch(request) {
    const body = await request.json();
    const response = await fetch('https://api.deepseek.com/v1/chat/completions', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer YOUR_API_KEY'
      },
      body: JSON.stringify(body)
    });
    return new Response(response.body, {
      headers: { 'Content-Type': 'application/json' }
    });
  }
};
```

---

## 📁 File Structure

```
/
├── chat.html          # Main interface (single file)
└── README.md          # This file
```

---

## 💡 Tips

- **Keyboard shortcuts**: Press `Enter` to send, `Shift+Enter` for new line.
- **File upload**: Drag and drop files into the chat area.
- **Parameters**: Click the "Parameters" button to adjust model settings.
- **Share**: Use the "Share" button to export conversations.

---

## ⚠️ Security Note

This is a **frontend-only** application. API keys should **never** be stored in the frontend code. Always use a backend proxy to protect your API keys.

---

## 📄 License

For learning and personal use only.

---

## 👤 Author

因式分解x · RSC Community

---

## 🙏 Acknowledgments

- Built with [marked](https://marked.js.org/) for Markdown rendering
- [KaTeX](https://katex.org/) for formula support
- [highlight.js](https://highlightjs.org/) for code highlighting
- Icons by [Font Awesome](https://fontawesome.com/)