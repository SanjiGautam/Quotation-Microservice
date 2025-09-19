from fastapi import FastAPI
from schema import QuotationRequest, QuotationResponse
from utils import calculate_quote, generate_email

app = FastAPI(title="Quotation Microservice")

@app.post("/quote", response_model=QuotationResponse)
def create_quote(req: QuotationRequest):
    quote = calculate_quote(req)
    email_draft = generate_email(req, quote)
    return {**quote, "email_draft": email_draft}
