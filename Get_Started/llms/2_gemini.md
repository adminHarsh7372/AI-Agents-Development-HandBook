# 🔷 Using Gemini (Google) in AI Agents

**Gemini** is Google’s family of LLMs (previously Bard), designed to compete directly with OpenAI’s GPT models. It’s powerful, fast, and integrates beautifully with other Google services.

If you’re already using Google Workspace (Gmail, Drive, Calendar), Gemini can be a strong choice for your agent workflows.

---

## 🧠 Why Use Gemini?

- 🔗 Native integration with Google tools
- 🤖 Great for text, code, and logic-based tasks
- 🔐 Built-in privacy, powered by Google Cloud
- ⚡ Available via Gemini API and Google AI Studio

---

## 🛠️ Gemini Model Variants

| Model         | Description                         | Use Case Examples               |
|---------------|-------------------------------------|----------------------------------|
| `Gemini 1.5 Pro` | Multimodal, strong performance      | Smart agents, long documents     |
| `Gemini Nano`   | Lightweight, for mobile devices     | On-device agents (Edge AI)       |

> Use **Gemini 1.5 Pro** via API for most agent applications.

---

## 🔑 How to Set Up Gemini API

1. Go to: [https://makersuite.google.com/app](https://makersuite.google.com/app)
2. Sign in and get access to the Gemini API
3. Grab your API key
4. Add it to your `.env` file:
>**GOOGLE_API_KEY=xxxxxxxxxxxxxxx*


---

## ⚙️ Basic Python Setup (With LangChain)

LangChain now supports Gemini via `ChatGoogleGenerativeAI`.

```python
from langchain_google_genai import ChatGoogleGenerativeAI

llm = ChatGoogleGenerativeAI(
 model="gemini-1.5-pro",
 temperature=0.3
)

response = llm.invoke("Give me a summary of this calendar event...")
print(response)
```
---

### 🔌 Gemini Strengths in Agents
**Gemini is especially useful when:**

- Your agents work inside the Google ecosystem (Gmail, Calendar, etc.)
- You need long context handling
- You want multimodal input (text + image)

### 📉 Rate Limits & Pricing (2025 Estimates)
| Model Name                                    | Use Case / Plan                               | Price (Approximate)                                  | Notes                                                                                                                                                                                                                                                                                                                                                                                           |
| :-------------------------------------------- | :-------------------------------------------- | :--------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Gemini 1.0 Pro** | Free Tier (API) / Gemini Free (Individual)    | $0 (Free Forever) / $0 (Free Forever)                | Available in the free tier for API usage with lower rate limits for testing. Also accessible via the "Gemini Free" plan for individuals for light tasks.                                                                                                                                                                                                                          |
| **Gemini 1.5 Pro** | Gemini Advanced (Individual) / API            | $19.99/month (via Google One AI Premium) / Varies by tokens | For individuals, bundled with Google One AI Premium, offering advanced features and integrations. For API usage, pricing is based on tokens: approx. $0.007 per 1K input tokens, $0.021 per 1K output tokens (prices can vary based on context window size and prompt length).                                                                                                              |
| **Gemini 1.5 Flash** | API                                           | Varies by tokens                                     | Optimized for fast and versatile performance. Pricing for API usage is approximately $0.00001875 per 1K input characters and $0.000075 per 1K output characters (for prompts <= 128k tokens).                                                                                                                                                                                       |
| **Gemini 2.0 Flash** | API                                           | Varies by tokens                                     | Newer multimodal model with improved capabilities and speed.                                                                                                                                                                                                                                                                                                                      |
| **Gemini 2.0 Flash-Lite** | API                                           | Varies by tokens                                     | Designed for cost-efficiency and speed. Pricing for API usage is approximately $0.10 per 1M input tokens and $0.40 per 1M output tokens.                                                                                                                                                                                                                                           |
| **Gemini 2.5 Pro** | Gemini Advanced (Individual) / API            | Included in Gemini Advanced / Varies by tokens       | Google's most advanced reasoning model for complex tasks. Available to Gemini Advanced users and for API usage (pricing similar to 1.5 Pro, often higher for reasoning/thinking capabilities).                                                                                                                                                                                          |
| **Gemini 2.5 Flash** | API                                           | Varies by tokens                                     | Offers a balance between price and performance. Pricing for API usage is approximately $0.30 per 1M input tokens and $2.50 per 1M output tokens.                                                                                                                                                                                                                                     |
| **Gemini 2.5 Flash-Lite (Experimental/Preview)** | API                                           | Varies by tokens                                     | Most cost-effective for high throughput tasks. Pricing for API usage is approximately $0.10 per 1M input tokens and $0.40 per 1M output tokens.                                                                                                                                                                                                                                     |
| **Gemini for Workspace – Business** | Business/Teams                                | $20/user/month (with 1-year commitment)              | Integrates AI features into Google Workspace apps like Gmail, Docs, Sheets. Does not include Gemini 1.5 Pro.                                                                                                                                                                                                                                                                 |
| **Gemini for Workspace – Enterprise** | Large Teams/Enterprise                        | $30/user/month (with 1-year commitment)              | Includes full Gemini 1.5 Pro access, Meet AI summaries, and enterprise-grade security.                                                                                                                                                                                                                                                                                       |
| **Google AI Ultra** | Individual (Premium)                          | $249.99/month ($124.99/month for 3 months promo)    | Offers highest limits and exclusive access to 2.5 Pro Deep Think, Veo 3 (video generation), and other premium features in creative AI tools.                                                                                                                                                                                                                                    |

>Gemini offers high token limits — great for long documents, full email threads, or meetings.

### ✅ Best Practices
**Use Gemini with Composio or LangChain to connect to Google tools**

Reduce hallucination by giving clear instructions

Use prompt templates and examples in Google AI Studio

### 🧩 When to Choose Gemini Over OpenAI
**Use Gemini when:**
- Gmail/Drive integration. 
- Multimodal tasks (text + image). 
- Mobile or on-device agents	. 
- Reasoning-heavy workflow. 
- Large code generation.

### 📌 Summary
Gemini is a strong alternative to OpenAI — especially if you're already using Google tools or want better support for long inputs.

**For Gmail agents, calendar workflows, or document parsing — Gemini just makes sense.**

>***→ Next: [Explore Groq LLMs »](3_groq.md)***