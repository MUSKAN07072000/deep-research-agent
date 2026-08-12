# Deep Research Agent 🧠🔍

An autonomous, multi-step search agent that executes iterative planning, ReAct reasoning, web tool execution, and dynamic context denoising to answer complex information-seeking queries.

---

## ✨ Core Features

- **ReAct Reasoning Loop:** Iteratively decides when to search, visit web pages, or synthesize final answers.
- **Multi-Step Search & Tool Calling:** Performs multi-hop searches to solve complex, multi-layered research queries.
- **Trajectory Denoising:** Automatically compresses and cleans search histories to prevent token overflow during long-horizon tasks.
- **LLM-Agnostic Interface:** Built with support for OpenAI, Google Gemini, and open-weight models.
- **Structured Synthesis:** Generates verified research reports complete with clear markdown citations.

---

## 🏗️ Architecture & Pipeline

```text
User Query
    │
    ▼
┌─────────────────────────┐
│  ReAct Reasoning Loop   │
└────────────┬────────────┘
             │
             ├──► [ Tool Execution: Search / Visit Page ]
             │            │
             │            ▼
             │   [ Raw Search Context ]
             │            │
             │            ▼
             └── [ Context Denoising ]
             │
             ▼
[ Final Synthesized Report ]



deep-research-agent/
├── eval/                    # Evaluation scripts
│   ├── eval.py             # Main evaluation benchmark script
│   ├── generate_answer.py  # Trajectory & response generation
│   └── prompt.py           # Evaluation prompt templates
├── src/                     # Core source code
│   ├── agent.py            # ReAct agent loop implementation
│   ├── memory.py           # Context history & denoising engine
│   ├── config.py           # Configuration & system prompts
│   └── tools/              # Agent tools
│       ├── search.py       # Web search tool
│       └── visit.py        # Page reader & scraper
├── main.py                  # CLI entry point
├── setup_env.sh             # API key & environment setup script
├── requirements.txt         # Project dependencies
├── .gitignore               # Git ignore configuration
└── README.md                # Technical documentation


step -1 : Installation 

# Clone repository
git clone [https://github.com/MUSKAN07072000/deep-research-agent.git](https://github.com/MUSKAN07072000/deep-research-agent.git)
cd deep-research-agent

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt


step-2 : Configure Environment Variables
Create a setup_env.sh or .env file in the root directory:
export OPENAI_API_KEY="your-openai-key"
export GEMINI_API_KEY="your-gemini-key"
export TAVILY_API_KEY="your-tavily-key"
Activate the environment variables:
source setup_env.sh

step-3 :  Run the Research Agent
Execute a multi-step deep research task via CLI:
python3 main.py --query "Analyze the architectural trade-offs of Mixture-of-Experts (MoE) models."

Evaluation & Benchmarking
Run automated evaluation scripts against datasets to test research accuracy and context management:
# Generate answer trajectories for evaluation tasks
python3 eval/generate_answer.py \
    --dataset_path data/questions.jsonl \
    --out_dir outputs/run_1 \
    --max_workers 10

# Evaluate the generated results
python3 eval/eval.py \
    --data_path outputs/run_1/results.jsonl \
    --max_workers 5


