# -------- Base stage --------
FROM python:3.10-slim AS base
WORKDIR /app

# -------- Builder stage --------
FROM base AS builder
COPY requirements.txt .
RUN pip install --upgrade pip && pip install --user -r requirements.txt

# -------- Final stage --------
FROM base AS final
COPY --from=builder /root/.local /root/.local
ENV PATH=/root/.local/bin:$PATH

COPY app ./app
EXPOSE 8000
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]

