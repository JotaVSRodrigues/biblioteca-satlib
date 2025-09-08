# 📚 Biblioteca Digital Escolar

Aplicação web para **gestão e acesso a livros digitais** (PDF e EPUB) por alunos e **tombamento/registro de obras físicas** pela administração da escola.  
Este projeto serve como base de estudo e implementação prática com **Java + Spring Boot**, **React/Next.js**, **MySQL** e **Docker**.

---

## 🎯 Objetivos

- Permitir que **alunos** cadastrem e acessem livros em **PDF/EPUB**.
- Disponibilizar **busca e filtros** eficientes por título, autor, gênero e palavras-chave.
- Oferecer ao **administrador** um sistema de **tombamento** de livros físicos (registro com metadados).
- Fornecer uma arquitetura simples de operar e evoluir.

---

## 📝 Funcionalidades

- Cadastro de livros com:
  - Título  
  - Gênero  
  - Autor  
  - Data de lançamento  
  - **Data de tombamento** (registro interno)  
  - Quantidade de páginas  
  - Editora  
  - Sinopse  
  - Arquivo **PDF** ou **EPUB**

- Busca (texto livre) e filtros (gênero, autor), com paginação e ordenação.
- Download controlado dos arquivos cadastrados.
- Área administrativa para tombamento e gerenciamento.
- Autenticação básica de admin (MVP; pode evoluir para múltiplos perfis).

---

## 🏗️ Arquitetura

- **Front-end:** React / Next.js (UI leve e responsiva).  
- **Back-end:** Java **Spring Boot** (API REST, validação, segurança, JPA).  
- **Banco de Dados:** **MySQL 8** (relacional, InnoDB).  
- **Armazenamento de Arquivos:** sistema de arquivos local (MVP) → opcional migrar para S3/MinIO.  
- **Containerização:** **Docker** e **Docker Compose**.

> **Por que MySQL?** Estável, amplamente suportado, Full-Text Search nativo (InnoDB) e ótimo custo-benefício em hospedagens gerenciadas.

---

## 🗃️ Modelo de Dados (resumo)

### Book
- `id` (UUID)  
- `title`, `genre`, `authorName`, `publisher`, `synopsis`  
- `releaseDate` (DATE), `registeredAt` (DATE)  
- `pages` (INT)  
- `filePath` (caminho local do PDF/EPUB)  
- `createdAt`, `updatedAt`

### User (ADMIN no MVP)
- `id`, `email`, `passwordHash`, `role`

---

## 🔌 Endpoints (MVP)

- `GET /api/books` → lista com filtros (`q`, `genre`, `author`, `sort`, `page`, `size`)  
- `GET /api/books/{id}` → detalhes  
- `GET /api/books/{id}/download` → download seguro do arquivo  
- `POST /api/books` → **ADMIN**: cadastro (multipart: `meta` + `file`)  
- `DELETE /api/books/{id}` → **ADMIN**

---
