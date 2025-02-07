# Supabase

## Prerequisite

1. Register an account for [Supabase](https://supabase.com/)
2. Click **New project**\\

![](<../.gitbook/assets/image (14).png>)

![](<../.gitbook/assets/image (25).png>)

1. Input required fields\
   **Name**, name of the project to be created. (e.g. convosuite)\
   **Database** Password, password to your postgres database. (e.g. click **Generate a password**)\\

![](<../.gitbook/assets/image (17).png>)

1. Click **Create new project** and wait for the project to finish setting up
2. Click **SQL Editor**\\

![](<../.gitbook/assets/image (20).png>)

1. Click **New query**\\

![](<../.gitbook/assets/image (24).png>)

1.  Copy & Paste [query ](https://js.langchain.com/docs/modules/indexes/vector\_stores/integrations/supabase#create-a-table-and-search-function-in-your-database)and run it by `Ctrl + Enter` or click **RUN**\
    **Table name**: documents\
    **Query name**: match\_documents

    ```plsql
    -- Enable the pgvector extension to work with embedding vectors
    create extension vector;

    -- Create a table to store your documents
    create table documents (
      id bigserial primary key,
      content text, -- corresponds to Document.pageContent
      metadata jsonb, -- corresponds to Document.metadata
      embedding vector(1536) -- 1536 works for OpenAI embeddings, change if needed
    );

    -- Create a function to search for documents
    create function match_documents (
      query_embedding vector(1536),
      match_count int DEFAULT null,
      filter jsonb DEFAULT '{}'
    ) returns table (
      id bigint,
      content text,
      metadata jsonb,
      similarity float
    )
    language plpgsql
    as $$
    #variable_conflict use_column
    begin
      return query
      select
        id,
        content,
        metadata,
        1 - (documents.embedding <=> query_embedding) as similarity
      from documents
      where metadata @> filter
      order by documents.embedding <=> query_embedding
      limit match_count;
    end;
    $$;

    ```

## Setup

1. Click **Project Settings**\Project Setting
2. Get your **Project URL & API Key**

![](<../.gitbook/assets/image (28).png>)

1. Copy & Paste each details (_API Key, URL, Table Name, Query Name_) into **Supabase Upsert Document** node or **Supabase Load Existing** node\
   ![](<../.gitbook/assets/image (21) (1) (1).png>)![](<../.gitbook/assets/image (29) (1).png>)
2. **Document** can be connect with any node under [**Document Loader**](../document-loaders.md) category
3. **Embeddings** can be connect with any node under [**Embeddings** ](../embeddings.md)category

## Resources

* [LangChain JS Supabase](https://js.langchain.com/docs/modules/indexes/vector\_stores/integrations/supabase)
* [Supabase Blog Post](https://supabase.com/blog/openai-embeddings-postgres-vector)
