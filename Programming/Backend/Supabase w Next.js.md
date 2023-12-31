> **Title**: Supabase w Next.js
> **Date**: 2023 - 8th Sep
> **Tags**: #Backend #NextJS #Supabase #PostgreSQL #SQL #database
---
Following [this](https://vercel.com/templates/next.js/supabase) tutorial, injecting this code to initialize the PostgreSQL database:
```SQL
create table if not exists todos (
id uuid default gen_random_uuid() primary key,
created_at timestamp with time zone default timezone('utc'::text, now()) not null,
title text,
is_complete boolean default false,
user_id uuid references auth.users default auth.uid()
);
  
-- Set up Row Level Security (RLS)
-- See https://supabase.com/docs/guides/auth/row-level-security for more details.
alter table todos
enable row level security;

create policy "Authenticated users can select todos" on todos
for select to authenticated using (true);

create policy "Authenticated users can insert their own todos" on todos
for insert to authenticated with check (auth.uid() = user_id);
```
This is a function that creates a table `todos` (if it doesn't exists already). It generates an initial schema with these columns:
- **id**: set as *primary key*. It is a UUID (Universally Unique Id), a 128bit value. Most likely no value will be provided, so it defaults to a `gen_random_uuid()` function that will fulfill the value type.
- **created_at**: timestamp value (`2023-09-08 10:30:00 UTC`)
- **title**: text value.
- **is_complete**: boolean that defaults to false
- **user_id**: a UUID column. `reference` is a keyword that references the value of another table, in this case `auth.users`. It defaults to `auth.uid()`, a *Supabase* function that retrieves the unique id of the authenticated user. This establishes a relationship between user_id and auth.
 This is 
- **auth.users**: