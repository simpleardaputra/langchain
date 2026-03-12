# Personal Notes - LangChain + Carbon AI

Used at Simple for building invoice-to-carbon-accounting AI pipeline.

## Invoice Processing Pipeline
```python
from langchain_openai import ChatOpenAI
from langchain.prompts import ChatPromptTemplate
from langchain_core.output_parsers import JsonOutputParser

llm = ChatOpenAI(model="gpt-4o", temperature=0)
prompt = ChatPromptTemplate.from_template(
    "Extract carbon emissions data from this invoice: {invoice_text}"
)
chain = prompt | llm | JsonOutputParser()
result = chain.invoke({"invoice_text": invoice_content})
```

## Article Library Pattern (30-40% token reduction)
- Cache embeddings for repeated invoice types
- Use smaller models for classification, GPT-4 only for extraction
- Chunk invoices by section, not fixed tokens

## Notes
- LangGraph for multi-step document validation workflows
- Always validate structured output with Pydantic before DB insert
