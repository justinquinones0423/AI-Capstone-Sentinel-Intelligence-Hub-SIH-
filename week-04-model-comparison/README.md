# Week 4: Model Comparison

Tested 4 AI models on 5 cybersecurity text samples to evaluate their suitability for the Alert Triage component.

## Models Tested
- **HF Sentiment** (distilbert-base-uncased-finetuned-sst-2-english)
- - **HF Zero-Shot** (facebook/bart-large-mnli)
  - - **HF NER** (dslim/bert-large-NER)
    - - **Groq Llama 3 8B** (Groq Cloud API)
     
      - ## Key Finding
      - **Recommended: Groq Llama 3 8B** for the Alert Triage component because it provides context-aware severity classification (CRITICAL, HIGH, MEDIUM, LOW, INFORMATIONAL) that directly aligns with SOC analyst workflow and includes reasoning for each classification decision.
     
      - ## Results Summary
      - - All 4 models achieved 100% agreement on threat vs. routine classification across 5 test cases
        - - Sentiment analysis provided fastest binary filtering (NEGATIVE/POSITIVE)
          - - Named Entity Recognition extracted relevant security indicators (IPs, emails, equipment)
            - - Groq LLM delivered domain-specific reasoning critical for audit trails and decision justification
             
              - ## Files
              - - `report.md` - Full analysis and findings
                - - `workflow.json` - n8n workflow export
                  - - `results/comparison-table.csv` - Airtable export with all model outputs
                   
                    - See `report.md` for detailed analysis, failure cases, and limitations.
