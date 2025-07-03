FROM node:20-slim

WORKDIR /app

# Copy package files first for better layer caching
COPY package*.json ./

# Install build dependencies for node-gyp
RUN apt-get update && apt-get install -y --no-install-recommends \
    python3 \
    make \
    g++ \
    build-essential \
    pkg-config \
    libcairo2-dev \
    libpango1.0-dev \
    libjpeg-dev \
    libgif-dev \
    librsvg2-dev \
    && rm -rf /var/lib/apt/lists/*

RUN npm install

# Copy the frontend code
COPY . .

# Recibe las variables como argumentos en tiempo de build
ARG NEXT_PUBLIC_SUPABASE_URL
ARG NEXT_PUBLIC_SUPABASE_ANON_KEY

# Las define como variables de entorno en el build (¡crucial para Next!)
ENV NEXT_PUBLIC_SUPABASE_URL=https://prndnensxpuqoaixklkx.supabase.co
ENV NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InBybmRuZW5zeHB1cW9haXhrbGt4Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NDkwOTE0OTEsImV4cCI6MjA2NDY2NzQ5MX0.bv95T9DsahDOKBxBpSRV12GzVrcQe3IWdI8qREj4-L0
ENV NEXT_PUBLIC_VERCEL_ENV production
# Imprimir variables en el log
RUN echo "NEXT_PUBLIC_SUPABASE_URL=$NEXT_PUBLIC_SUPABASE_URL"
RUN echo "NEXT_PUBLIC_SUPABASE_ANON_KEY=$NEXT_PUBLIC_SUPABASE_ANON_KEY"
RUN npm run build

EXPOSE 3000

# Default command is dev, but can be overridden in docker-compose
CMD ["npm", "start"]
