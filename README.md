# Wikipedia + Gemini AI Chat System

A Python application that scrapes any Wikipedia page and creates an interactive AI-powered chat system using Google's Gemini API. Ask questions, get summaries, and have natural conversations about any Wikipedia topic!

## Features

- 📥 **Smart Wikipedia Scraping**: Extracts clean content from any Wikipedia page
- 🤖 **AI-Powered Conversations**: Uses Google's Gemini AI for intelligent responses
- 💬 **Interactive Chat**: Have natural conversations about the scraped content
- 📊 **Auto-Generated Overviews**: Get AI summaries of Wikipedia articles
- 🎯 **Context-Aware**: AI uses the Wikipedia content as its knowledge base

## Setup

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Get Gemini API Key

1. Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Sign in with your Google account
3. Click "Create API Key"
4. Copy your API key

### 3. Set API Key

**Option A: Environment Variable (Recommended)**
```bash
export GEMINI_API_KEY='your-api-key-here'
```

**Option B: Pass Directly in Code**
```python
chat_system = WikipediaGeminiChat(api_key='your-api-key-here')
```

## Usage

### Quick Start

```python
from wikipedia_gemini_chat import WikipediaGeminiChat

# Initialize the system
chat = WikipediaGeminiChat()

# Run full pipeline with any Wikipedia URL
url = "https://en.wikipedia.org/wiki/Artificial_intelligence"
chat.run_full_pipeline(url, interactive=True)
```

### Run the Script Directly

```bash
python wikipedia_gemini_chat.py
```

Then enter any Wikipedia URL when prompted!

### Programmatic Usage

```python
from wikipedia_gemini_chat import WikipediaGeminiChat

# Initialize
chat = WikipediaGeminiChat()

# Scrape Wikipedia page
content = chat.scrape_wikipedia("https://en.wikipedia.org/wiki/Python_(programming_language)")

# Initialize AI chat with content
chat.initialize_chat()

# Get AI overview
overview = chat.get_overview()
print(overview)

# Ask specific questions
response = chat.ask_question("What are the main features of Python?")
print(response)

response = chat.ask_question("Who created Python and when?")
print(response)

# Start interactive chat
chat.interactive_chat()
```

## Example Session

```
📥 Fetching data from Wikipedia...
   URL: https://en.wikipedia.org/wiki/Artificial_intelligence
✅ Successfully scraped Wikipedia page!
   Title: Artificial intelligence
   Content length: 15240 characters
   Paragraphs extracted: 45

🤖 Initializing Gemini AI chat...
✅ Chat initialized! You can now ask questions about: Artificial intelligence

📊 AI-Generated Overview:
----------------------------------------------------------------------
**Summary:** Artificial intelligence (AI) is intelligence demonstrated 
by machines, in contrast to natural intelligence displayed by humans. 
It's a broad field encompassing various approaches to creating systems 
capable of performing tasks that typically require human intelligence.

**Key Points:**
• AI involves creating systems that can learn, reason, and solve problems
• Major subfields include machine learning, deep learning, and natural 
  language processing
• AI has applications in healthcare, finance, transportation, and more
• Ethical concerns include bias, job displacement, and autonomous weapons
• The field has experienced multiple "AI winters" but is now rapidly advancing

**Significance:** AI is transforming nearly every aspect of modern life...
----------------------------------------------------------------------

💬 Interactive Chat about: Artificial intelligence
======================================================================
Commands:
  - Type your question and press Enter
  - Type 'overview' for an AI summary
  - Type 'quit' or 'exit' to end the chat
  - Type 'url' to see the Wikipedia page URL
======================================================================

You: What is machine learning?

🤖 AI: Machine learning is a subset of artificial intelligence that 
enables systems to learn and improve from experience without being 
explicitly programmed. It uses algorithms that can identify patterns 
in data and make predictions or decisions based on that data...

You: How is AI used in healthcare?

🤖 AI: AI has numerous applications in healthcare, including...
```

## Interactive Commands

While in chat mode:
- **Type any question** - Ask about the Wikipedia topic
- **`overview`** - Get an AI-generated summary
- **`url`** - Display the Wikipedia page URL
- **`quit`** or **`exit`** - End the chat session

## Example Wikipedia URLs to Try

```python
# Technology
"https://en.wikipedia.org/wiki/Artificial_intelligence"
"https://en.wikipedia.org/wiki/Python_(programming_language)"
"https://en.wikipedia.org/wiki/Blockchain"

# Science
"https://en.wikipedia.org/wiki/Climate_change"
"https://en.wikipedia.org/wiki/Quantum_mechanics"
"https://en.wikipedia.org/wiki/COVID-19_pandemic"

# History
"https://en.wikipedia.org/wiki/World_War_II"
"https://en.wikipedia.org/wiki/Ancient_Rome"
"https://en.wikipedia.org/wiki/Renaissance"

# Geography
"https://en.wikipedia.org/wiki/Mount_Everest"
"https://en.wikipedia.org/wiki/Amazon_rainforest"
"https://en.wikipedia.org/wiki/Sahara"
```

## API Information

### Gemini API
- **Free Tier**: 60 requests per minute
- **Model Used**: gemini-pro (optimized for text)
- **Context Window**: Up to 30,720 tokens
- **Get API Key**: [Google AI Studio](https://makersuite.google.com/app/apikey)

## How It Works

1. **Web Scraping**: Uses BeautifulSoup to extract clean text from Wikipedia
2. **Content Processing**: Removes navigation, references, and formatting
3. **AI Context Loading**: Feeds the Wikipedia content to Gemini AI
4. **Interactive Chat**: Maintains conversation history for context-aware responses

## Troubleshooting

### "API key required" Error
Make sure you've set your Gemini API key:
```bash
export GEMINI_API_KEY='your-api-key-here'
```

### "Failed to scrape Wikipedia" Error
- Check your internet connection
- Verify the Wikipedia URL is valid and accessible
- Some pages with complex structures might need adjustments

### "Rate limit exceeded" Error
The free tier allows 60 requests per minute. Wait a moment before continuing.

## Customization

### Adjust Content Length
Modify the scraping parameters in `scrape_wikipedia()`:
```python
combined_content = '\n\n'.join(full_text[:30])  # Get 30 paragraphs instead of 20
```

### Change AI Model
Use a different Gemini model:
```python
self.model = genai.GenerativeModel('gemini-pro')  # or 'gemini-1.5-pro'
```

### Custom System Prompts
Modify the `initialize_chat()` method to customize how the AI responds.

## Advanced Features

### Non-Interactive Mode
```python
chat = WikipediaGeminiChat()
chat.run_full_pipeline(url, interactive=False)

# Then ask questions programmatically
answer1 = chat.ask_question("What is the main topic?")
answer2 = chat.ask_question("Tell me more about...")
```

### Batch Processing
```python
urls = [
    "https://en.wikipedia.org/wiki/Topic1",
    "https://en.wikipedia.org/wiki/Topic2",
    "https://en.wikipedia.org/wiki/Topic3"
]

chat = WikipediaGeminiChat()

for url in urls:
    content = chat.scrape_wikipedia(url)
    chat.initialize_chat()
    overview = chat.get_overview()
    print(f"\n{content['title']}:\n{overview}\n")
```

## License

MIT License - Feel free to use and modify!

## Contributing

Contributions welcome! Feel free to:
- Add new features
- Improve scraping logic
- Enhance AI prompts
- Fix bugs

## Credits

- **Google Gemini API**: AI-powered conversations
- **Wikipedia**: Content source
- **BeautifulSoup**: Web scraping
